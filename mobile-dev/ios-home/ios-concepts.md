---
description: Notes from reading Apple's View Controller Programming guide.
---

# ViewController Concepts

## Role of ViewControllers

Source: Apple's [View Controller Programming guide](https://developer.apple.com/library/archive/featuredarticles/ViewControllerPGforiPhoneOS/).

* View Controller manages a portion of the application's user interface and its interaction with the underlying data. They also coordinate the transition between other parts of your UI.
* Every view controller has a **single root view** to which you can add more views.
* **UIViewController** class manages the views, handles events, transitions to other view controllers, coordinates with other parts of the app.
* 2 type of view controllers:
  * **Content view controllers** - manages a specific part of the app's content
  * **Container view controllers** - has child view controllers and present them or facilitate navigation between them. Manages its own views \(root view and sub views\) as well as the _root views_ of its child view controllers. It does not manage the content of its children; just the size and position of the _root view of those children_. Example: **UINavigationController, UISplitViewController**
* There should be a clean separation between view controllers and data objects:
  * Data objects - contain logic to ensure integrity of data and manage the data
  * View controllers - validate inputs coming from views, package it in a way that the data objects understand and the reverse. Use _UIDocument_ object to read and write data to persistent store.
* Event Handling - View controllers are responder objects that handle events using delegate methods or action methods on the views
* View controller owns all the views and any objects it creates. View-related objects will be automatically released by UIKit; but any objects explicitly created by View Controller should be managed by the view controller itself.
* View controllers should present the views and adapt the presentation to match the underlying environment.
* **Coarse-grained changes** and **fine-grained changes**:
  * coarse-grained changes happen when view controller's traits change. Traits are attributes that describe the overall environment like display scale. Two important traits - view controller's horizontal size class and vertical size class
  * fine-grained changes happen within given size class, for example when user rotates the device, the size class remains the same, but the screen dimensions change. Most of the time, using AutoLayout is sufficient to ensure that the views adjust themselves.

## View Controller Hierarchy

* You should maintain the relationship between the view controllers as prescribed by UIKit to ensure that the automatic behaviors are delivered to the correct view controllers properly at runtime.
* **Root View Controller** - This is the anchor of the view controller hierarchy. It defines the initial content seen by the user. Every window has exactly one root view controller. Window does not have any content of its own; the root view controller's content fills the window. Available as the property **rootViewController** of the **UIWindow** object.
* **Container view controllers** - allows you to assemble complex UI from other view controllers. For eg: UINavigationController displays the content from a child view controller along with a navigation bar and toolbar. Container VCs are often installed as root VCs, but can also be presented modally or a children of other container VCs.
  * Some container controllers will not remove their child view controllers when it presents other view controllers. For example, navigation controller does not remove its child view controllers when a new VC is pushed to the stack.
  * You can implement a custom container view controller by explicitly adding and removing child view controllers. See details in [https://developer.apple.com/library/archive/featuredarticles/ViewControllerPGforiPhoneOS/ImplementingaContainerViewController.html](https://developer.apple.com/library/archive/featuredarticles/ViewControllerPGforiPhoneOS/ImplementingaContainerViewController.html)
* **Presented view controllers** - Presenting a view controller replaces the contents of the current view controller with the contents of the new VC, usually hiding the contents of current VC.
  * Usually used to present a UI as a modal; also used to build the application UI
  * when you present a VC, UIKit creates relationships between presented view controller and presenting view controller. See these properties in UIViewController.h
    * **presentedViewController** - the view controller that this view controller presented
    * **presentingViewController** - the view controller that presented this view controller
  * When you present a VC, UIKit looks for a view controller that can provide the context for presentation. Usually this is provided by a nearest container VC or the root VC or you can tell which view controller will handle the presentation context.
  * When a child VC of a navigation control asks UIKit to present a VC in full screen presentation style, the navigation controller provides the presentation context \(instead of the child VS who initiated the request\) so that the child VC doesn't have to know the bounds of the container.

## Guidelines and Best Practices

1. Use system supplied View Controllers - makes it easy to use and provides consistent experience to the user. eg: standard container view controllers like UINavigationController, UISplitViewController etc., UIImagePickerController in UIKit, contact info view controllers in Address Book UI f/w.
2. Do not modify the view hierarchy of system-provided view controllers.
3. Make each view controller an island - View controllers should not know about the internal workings or view hierarchy of other view controllers. If two VCs want to communicate with each other, do it using explicitly defined public headers, preferably using delegation design pattern.
4. Use the root view of your View Controller only as a container for other views. This will ensure that all views have a common root view and makes Auto Layout operations correct and simpler.
5. Know where your data lives - have a clean separation of responsibilities between view controller and data objects. VC's main responsibility is to ensure that its view contain correct info; it may save a cache of the data for performance or do validation of data; but it should never deal with managing the data or ensuring integrity of the data - that is the responsibility of the data objects.
6. View controllers should adapt to different sizes of screens and respond to runtime changes in size and size classes.

