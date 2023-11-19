# Debugging Tricks

### See the Swift generated interface for Objective-C header file

If you are accessing an Objective-C class from Swift, you can see the Swift interface of the ObjC file:\
&#x20;  \- Open the header file in Xcode, eg: MyClass.h\
&#x20;  \- Press the square button on top left of the main editor ("Related Items") and choose **Counterparts**\
&#x20;  \- You will see the item "MyClass.h (Swift 4.2 Interface)". This file will show the Swift interface

### Send deep link to an app in a simulator

The target app's Info.plist should have the URL scheme `acj` registered. There should be a simulator running with the app installed.

```
xcrun simctl openurl booted "acj://message/1000"
```

### See Background Color in UI views

* Set a background color for all your UI views in the storyboard
* Add all those views to a an IBOutlet Referencing Outlet collections (right click and choose "New Ref Out Coll..."
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
