#SwiftConventions
This document is an attempt to collect and describe programming approaches that seem to be good candidates for Conventions in Swift Programming Language.

###Contributing 
To contribute: fork this project, edit and create a pull request.

#### General Swift Conventions
* use Value Types to represent data,
* use classes to describe logic
* laverage Touples to return more than just one value from a method (eg. result & error)

### Methods
There is a lots of new framework/language methods in Swift that are extremely short and at a first glance they are not self explanatory as they would be in objc.
A good convention is to have short clear function/method names for generic components that you use quite often and a bit more verbose self explanatory signatures for application wide methods.

##### Good example of generic methods:
```swift
func map<U>(transform: (T) -> U) -> Array<U>
``` 

##### Bad example of generic methods:
```swift
func arrayByEnumeratingObjectsUsingBlock(_ block: (AnyObject!) -> [AnyObject]
```

##### TODO: Application wide methods

### Initializer
In objc there was a good convention that in init method one should only have those parameters that couldn't be ommited while creating an object (it wouldn't make sense to create the object without setting one of them). Any other configurations that you could either have a default value for or it is an optional property - should be moved to @property and to be set right after initializing an object (when desired).

In swift it is not the case. We do have optionals, we still have parameter labels and you can also set default values to parameters.

> [...] So you could define the initializer like so:

```swift
init(contentRect: NSRect, styleMask: NSWindowMask = NSWindowMask.Titled, backing: NSBackingStoreType = .Buffered, defer: Bool = false, screen: NSScreen? = nil)
```
> Which reduces the initialization to short:

```swift
NSWindow(contentRect: frame)
```
> — [radex.io](http://radex.io/swift/methods/)

#### Optionals
##### Naming (TODO: prefix/suffix)
It sounds like a good idea to give a variable that is an Optional a name with some sort of prefix that would explicitly say it may contain nil eg.: "optionalFullName".

##### Binding
It looks better when Optional is binded using "if let" syntax rather than with Forced Unwrapping. This way you can in just one step unwrap the value and do something when the value is not missing:
```swift
if let a = optionalVal  {
    // a contains unwrapped value from optional
}
```

instead of:
```swift
let a = optionalVal!
```
