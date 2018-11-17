# Cocoapods Gotchas

## Warning about ALWAYS_EMBED_SWIFT_STANDARD_LIBRARIES when running `pod install`
When you run `pod install`, Cocoapods shows the following warning (usually this happens for projects that were recently moved to Cocoapods):
```
[!] The `URLSessionMockerSampleTests [Debug]` target overrides the 
`ALWAYS_EMBED_SWIFT_STANDARD_LIBRARIES` build setting defined in 
`Pods/Target Support Files/Pods-URLSessionMockerSampleTests/Pods-URLSessionMockerSampleTests.debug.xcconfig'. 
This can lead to problems with the CocoaPods installation
```
#### Root cause
This warning indicates that the build setting `ALWAYS_EMBED_SWIFT_STANDARD_LIBRARIES` that Cocoapods wants to manage has already been set in the Xcode settings and hence may conflict with Cocoapod's setting. You can find this setting in Xcode (go to Build settings of the target(s) mentioned in the warning message (in this case `URLSessionMockerSampleTests [Debug]`); look for the setting `Always Embed Swift Standard Libraries` in the section `Build Options`).

Usually, this warning appears when existing projects are converted to use Cocoapods, because this etting may already set in Xcode and now Cocoapods wants to manage it for all the frameworks that it brings into the app target. 

#### Solution
There are two options (as the warning also indicates) - either delete the build setting from the target OR modify the build setting in Xcode to `$(inherited)` so that the value set by Cocoapods will take precedence. You can do this as follows:
* In Xcode, go to the Target settings and find the build setting `Always Embed Swift Standard Libraries`
* Double click on the value (usually it is `YES`) so that a text popup appears
* Replace the text `YES` with the value `$(inherited)`
* Dismiss the text popup; make sure that the value is updated
* Run `pod install` again. It should run without any warnings

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



