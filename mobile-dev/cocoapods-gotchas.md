# Cocoapods Troubleshooting

### Cocoapods warning ALWAYS\_EMBED\_SWIFT\_STANDARD\_LIBRARIES

When you run `pod install`, Cocoapods shows the following warning \(usually this happens for projects that were recently moved to Cocoapods\):

```text
[!] The `URLSessionMockerSampleTests [Debug]` target overrides the 
`ALWAYS_EMBED_SWIFT_STANDARD_LIBRARIES` build setting defined in 
`Pods/Target Support Files/Pods-URLSessionMockerSampleTests/Pods-URLSessionMockerSampleTests.debug.xcconfig'. 
This can lead to problems with the CocoaPods installation
```

#### Root cause

This warning indicates that the build setting `ALWAYS_EMBED_SWIFT_STANDARD_LIBRARIES` that Cocoapods wants to manage has already been set in the Xcode settings and hence may conflict with Cocoapod's setting. You can find this setting in Xcode \(go to Build settings of the target\(s\) mentioned in the warning message \(in this case `URLSessionMockerSampleTests [Debug]`\); look for the setting `Always Embed Swift Standard Libraries` in the section `Build Options`\).

Usually, this warning appears when existing projects are converted to use Cocoapods, because this etting may already set in Xcode and now Cocoapods wants to manage it for all the frameworks that it brings into the app target.

#### Solution

There are two options \(as the warning also indicates\) - either delete the build setting from the target OR modify the build setting in Xcode to `$(inherited)` so that the value set by Cocoapods will take precedence. You can do this as follows:

* In Xcode, go to the Target settings and find the build setting `Always Embed Swift Standard Libraries`
  * Either select the settings and hit the Delete key so that it is removed from the project file 
  * OR click on the dropdown and select `Other..` so that a text popup appears. Set/replace the text with the value `$(inherited)`. Dismiss the text popup; make sure that the value is updated
* Run `pod install` again. It should run without any warnings

### Unit Tests Fail Without Executing

In some projects with specific Pods in Tests target, the tests will fail without even executing, i.e. Xcode test job shows "Test Failed" notification, but none of the tests would have executed. This happens even if there is only one empty test function in the whole project. The logs in Report navigator shows the following error:

```text
URLSessionMockerSample.app (32192) encountered an error (Early unexpected exit, operation never finished bootstrapping 
- no restart will be attempted. 
(Underlying error: The test runner exited with code 1 before checking in.))
```

I have seen this issue with a specific Cocoapod named `Mocker`. Here is the Podfile for that project:

```text
target 'URLSessionMockerSample' do
  target 'URLSessionMockerSampleTests' do
    inherit! :search_paths
    # Pods for testing
    pod 'Mocker'
  end
end
```

When I replaced `Mocker` pod with another Pod \(eg: `AFNetworking`\), the tests executed properly. There seems to something specific to that pod \(although I couldn't find anything special in its pod spec\).

Two workarounds I found for this problem were: 1. Add the offending pod outside the Tests target - as follows

```text
target 'URLSessionMockerSample' do
  pod 'Mocker'
  target 'URLSessionMockerSampleTests' do
    inherit! :search_paths
    # Pods for testing
  end
end
```

1. Change the structure of the Podfile such that the test targets are at the same level as the app target as follows:

   \`\`\`

   target 'URLSessionMockerSample' do

   end

target 'URLSessionMockerSampleTests' do

## inherit! :search\_paths

## Pods for testing

pod 'Mocker' end

```text
## Https Error while running `pod install`

```text
[!] 'AppDynamicsAgent' uses the unencrypted http protocol to transfer the Pod. 
Please be sure you're in a safe network with only trusted hosts in there. 
Please reach out to the library author to notify them of this security issue.
```

The podspec of that pod would have a `source` attribute which points to an HTTP url instead of HTTPS, for example here is a snippet from the [podSpec of AppDynamics](https://github.com/CocoaPods/Specs/blob/d0ec5a65e80656c8d78e12ff19f251df879e0bc2/Specs/0/b/f/AppDynamicsAgent/42.9.0/AppDynamicsAgent.podspec.json)

```text
  "source": {
    "http": "http://cdn.appdynamics.com/eum-mobile/iOSAgent-4.2.9.0.zip"
  },
```

