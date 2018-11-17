# iOS Gotchas

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
