---
description: iOS General concepts. Specific topics are described as sub-pages to this page.
---

# iOS

## ARC Retain Cycles

Source: [https://krakendev.io/blog/weak-and-unowned-references-in-swift](https://krakendev.io/blog/weak-and-unowned-references-in-swift)

* Strong reference - a reference that increments the reference count by 1 and thereby prevents the referring object to be deallocated by ARC. Strong references are safe to use when the object hierarchy is linear, i.e parent -&gt; child only
* Weak reference - reference that does not increment the ref count and thus does NOT protect the object from being deallocated by ARC. Good for child to refer to parent object - so when parent object goes out of scope, the child will also go out of scope automatically. In Swift, weak references have to be Mutable and Optional \(because it should be possible to be set to nil after initial value\). Use this for object-&gt; delegate relationship and for objects that use NSNotificationCenter, NSTimer etc.
* Retain cycle - Two objects have strong reference to each other. Both objects won't be deallocated.
* Unowned reference - a reference that does not increment ref count \(like weak reference\), but is not an Optional \(unlike weak reference\). Use this only when you are sure that the object that defines the reference \(for eg: closure\) and the object that it refers to \(instance that it captures\) will be deallocated at the same time. For example, lazily defined closure properties.



