# iOS Gotchas

### CocoaPods warning
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

### Keyboard does not appear on Simulator when you tap inside a text field

Root cause: One potential reason is that the hardware keyboard is enabled. You can confirm this by checking if NSNotification for keyboardWillShow and keyboardWillHide are mixed up \(i.e when you tap inside a text field, the notification keyboardWillHide is sent instead of keyboardWillShow\)

Solution: Press Cmd+K \(Toggle keyboard\) on the simulator window.

### Unnecessary vertical blank space at the top of UITableView {#unnecessary-vertical-blank-space-at-the-top-of-uitableview}

[https://stackoverflow.com/questions/18880341/why-is-there-extra-padding-at-the-top-of-my-uitableview-with-style-uitableviewst?utm\_medium=organic&utm\_source=google\_rich\_qa&utm\_campaign=google\_rich\_qa](https://stackoverflow.com/questions/18880341/why-is-there-extra-padding-at-the-top-of-my-uitableview-with-style-uitableviewst?utm_medium=organic&utm_source=google_rich_qa&utm_campaign=google_rich_qa)

### A table view looks crooked on iOS 10 only

* Check if the tableView's estimatedRowHeight is set. On iOS 10, it has to be set explicitly sometimes.

### Guidelines for LaunchDarkly FeatureFlag

**Problem: The flag value comes as the default value**

* Make sure that you are pointing to the same LD environment as the QBSE server environment
* Make sure that the Targeting is ON
* Make sure that the user is not excluded by any rule
* If you added a specific user-based rule, make sure that the userid is available in LD

### Neat Debugging Trick to send deep link to an app in a simulator
The target app's Info.plist should have the URL scheme `acj` registered. There should be a simulator running with the app installed.
``` 
xcrun simctl openurl booted "acj://message/1000"
```

### Neat Debugging Trick to See Background Color in UI views {#neat-debugging-trick-to-see-background-color-in-ui-views}

* Set a background color for all your UI views in the storyboard
* Add all those views to a an IBOutlet Referencing Outlet collections \(right click and choose "New Ref Out Coll..."
* Then in the viewDidLoad of your view controller, iterate through the colors and set the background color to clear

```swift
override func viewDidLoad\(\) {
  super.viewDidLoad\(\)

  // Clear background colors from labels and buttons.
  // backgroundColoredViews is a Reference Outlet collection created from the Storyboard

  for view in backgroundColoredViews {
    view.backgroundColor = UIColor.clear
  }
}
 ```
