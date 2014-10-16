#SwiftConventions
This document is an attempt to collect and describe programming approaches that seem to be good candidates for Conventions in Swift Programming Language.

###Contributing 
To contribute: fork this project, edit and create a pull request.

### Methods
There is a lots of new framework/language methods in Swift that are extreamly short and at a first glance they are not self explanatory as they would in objc.
A good convention is to have short clear function/method names for generic components that you use quite often and a bit more verbose self explanatory signatures for application wide methods.

##### Good example of generic methods:
```swift
func map<U>(transform: (T) -> U) -> Array<U>
``` 

##### Bad example of generic methods:
```swift
func arrayByEnumeratingObjectsUsingBlock(_ block: (AnyObject!) -> [AnyObject]
```
arrayByE

##### TODO: Application wide methods

### Initializer
In objc there was a good convention that in init method one should only have these parameters that can not be ommited while creating an object (it doesn't make sense to create an object without setting one of them). Any other configurations that you could either have a default value for or it is an optional property - should be moved to @property and to be set after initializing an object (if needed).

In swift it is not the case. We do have optionals, we still have parameter labels and...

> [...] you can set default values to parameters. So you could define the initializer like so:

```swift
init(contentRect: NSRect, styleMask: NSWindowMask = NSWindowMask.Titled, backing: NSBackingStoreType = .Buffered, defer: Bool = false, screen: NSScreen? = nil)
```
> Which reduces the initialization to short:

```swift
NSWindow(contentRect: frame)
```
> — [radex.io](http://radex.io/swift/methods/)