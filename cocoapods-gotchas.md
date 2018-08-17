# Cocoapods Gotchas

## Error while running `pod install`

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



