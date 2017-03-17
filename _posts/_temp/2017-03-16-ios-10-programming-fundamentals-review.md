### Pro
- Comprehensive
### Con
- The code isn't highlighted 


### Nested structures:

```swift
class Dog {
    struct Noise {
        static var noise = "Woof"
    }
	func bark() {
        print(Dog.Noise.noise)
	} 
}
//print(Dog.Noise.noise)//Woof
```

### Enums:

```swift
/*If the type is String, the implicitly assigned values are the string equivalents of the
case names. For example:*/
    enum Filter : String {
        case albums
        case playlists
        case podcasts
        case books
}
```


Even when there are only two states, an enum is often better than, say, a mere Bool, because the enum’s states have names. With a Bool, you have to know what true and false signify in a particular usage; with an enum, the name of the enum and the names of its cases tell you its significance. More‐ over, you can store extra information in an enum’s associated value or raw value; you can’t do that with a mere Bool.


### Struct:

Value Types and Reference Types
A major difference between enums and structs, on the one hand, and classes, on the other, is that enums and structs are value types, whereas classes are reference types.
A value type is not mutable in place, even though it seems to be. For example, con‐ sider a struct. A struct is a value type:

Now, Swift’s syntax of assignment would lead us to believe that changing a Digit’s number is possible:
But in reality, when you apparently mutate an instance of a value type, you are actually replacing that instance with a di erent instance. To see that this is true, add a setter observer:  
That explains why it is impossible to mutate a value type instance if the reference to that instance is declared with let:  

```swift
struct Digit {
    var number : Int
    init(_ n:Int) {
        self.number = n
    }
}

var d = Digit(123)

d.number = 42
Swift.print("d.number: " + "\(d.number)")

let d2 = Digit(123)
d2.number = 42 // compile error
```

### Class:

 Classes are not bad; they’re good! For one thing, a class instance is very efficient to pass around, because all you’re passing is a pointer. No matter how big and complicated a class instance may be, no matter how many prop‐ erties it may have containing vast amounts of data, passing the instance is incredibly fast and efficient, because no new data is generated.
 
 Even more important, there are many situations where the independent identity of a class instance, no matter how many times it is referred to, is exactly what you want. The extended lifetime of a class instance, as it is passed around, can be crucial to its functionality and integrity. In particular, only a class instance can successfully repre‐ sent an independent reality. For example, a UIView needs to be a class, not a struct, because an individual UIView instance, no matter how it gets passed around, must continue to represent the same single real and persistent view in your running app’s interface.