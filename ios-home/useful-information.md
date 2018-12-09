# Useful Information

#### How to check if a View Controller is Presented Modally or Pushed to Nav Stack

If you are presenting one VC directly on top of another VC, the property `isPresenting` will return true. If the VC is pushed to navigation stack, then the property will be false.

However, if the second VC is wrapped inside a UINavigationController before it was presented, then the property will return false and hence cannot be used. The better alternative is to check if the first view controller in the navigation stack is `self` - if so, it means that the second VC was presented modally through an intermediate navigation controller.

```swift
// If this view controller was presented modally (i.e. the first VC in its navigation 
//    stack is itself), then show the Cancel button
var isPresentedModally {
    if ((self.navigationController == nil) || 
         (self.navigationController.viewControllers.first == self)) {
        return true
    }
    return false
}
```

#### How to hide the "Back" button or the default back button text in the nav bar

If a view controller's title is ver long, when more view controllers are pushed to the this VC's navigation stack, the navigation bar of those view controllers will display the text "Back" instead of this view controller's title. In most cases, this results in inconsistent UI in the app.

So we can set the current view controller's back button title to be empty \(so that the nav bar will show just the green Left arrow\).

```swift
// Inside MyViewController.viewDidLoad(:).....
backNavButton = UIBarButtonItem(title: "", style: .plain, 
                                target: nil, action: nil)
self.navigationItem.backBarButtonItem = backNavButton
```

