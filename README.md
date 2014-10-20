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
Optionals are optional in Swift. In Objective-C it was a default, you were expected to handle nil values at any time. If this is no longer the case in Swift (nil is not a first-class construct), we shouldn't use them everywhere in Swift code as we had no choice. If we do then we loose its true meaning. Where shall we use optionals then?

* as a possible result of a methods that finds result in a collection when there is no result.
* to mark an end of sequence

It sounds like a good idea to give a variable that is an Optional a name with some sort of prefix/suffix that would explicitly say it may contain nil eg.: "optionalFullName".

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

On the other hand if you deside not to prefix variable name with "optional" you may find this kind of unwrapping cool:
```swift
if let x = x { // rebinding to the same identifier
 ... 
} 
```

##### Implicit unwrapping
IBOutlets are great model to use implicitly unwrapped optionals, they are conneced before "awakeFromNib" and we just use them as they weren't optionals since that time.

[http://nomothetis.svbtle.com/optionals-if-we-must](http://nomothetis.svbtle.com/optionals-if-we-must)
[http://airspeedvelocity.net/2014/08/08/the-case-against-making-array-subscript-optional/](http://airspeedvelocity.net/2014/08/08/the-case-against-making-array-subscript-optional/)

#### Touples
Can use switch statement together with touples to reduce number of "if else if" constructs eg.:
```swift
var error: NSError?
let json: AnyObject? = NSJSONSerialization.JSONObjectWithData(data, options: NSJSONReadingOptions(0), error: &error)

switch (json, error) {
case (_, .Some(let error)): return .Failure(error)
case (.Some(let json), _):  return .Success(json)
default :
}
```

#### Prefix, Infix, Suffix operators
These tools shouldnt be overused. Usually it ends up with less readable code for the begginers. However some generic solutions like simplified pattern matching are good candidates where prefix, infix or suffix operator will be an advantage

Consider writing
```swift
let answer = "-v" =~ /^(?:-[a-z]|--[a-z]\S*)$/
```

instead of:
```swift
let regex = NSRegularExpression(pattern:"^(?:-[a-z]|--[a-z]\\S*)$" 
                                options:nil,
                                  error:nil)

let match = regex.numberOfMatchesInString("-v", 
               options:nil
                 range:NSRange(location:0,
                                 length:countElements(testString))

let answer = match > 0
```

[http://nomothetis.svbtle.com/clean-regular-expressions-using-conversions](http://nomothetis.svbtle.com/clean-regular-expressions-using-conversions)

#### Error handling
###### TODO
http://nomothetis.svbtle.com/error-handling-in-swift
nested (result, error) results 
http://robnapier.net/functional-wish-fulfillment