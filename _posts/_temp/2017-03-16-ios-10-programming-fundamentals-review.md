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
 
 ### Enums
 
 Swift is chock full of protocols already. Let’s make one of our own object types adopt one. One of the most useful Swift protocols is CustomStringConvertible. The Cus‐ tomStringConvertible protocol requires that we implement a description String property. If we do that, a wonderful thing happens: when an instance of this type is used in string interpolation or print (or the po command in the console), the description property value is used automatically to represent it.
Recall, for example, the Filter enum, from earlier in this chapter. I’ll add a description property to it:
```swift
enum Filter : String {
    case albums = "Albums"
    case playlists = "Playlists"
    case podcasts = "Podcasts"
    case books = "Audiobooks"
    var description : String { return self.rawValue }
}
```
But that isn’t enough, in and of itself, to give Filter the power of the CustomString‐ Convertible protocol; to do that, we also need to adopt the CustomStringConvertible protocol formally. There is already a colon and a type in the Filter declaration, so an adopted protocol comes after a comma:
```swift
enum Filter : String, CustomStringConvertible {
    case albums = "Albums"
    case playlists = "Playlists"
    case podcasts = "Podcasts"
    case books = "Audiobooks"
    var description : String { return self.rawValue }
}
```
We have now made Filter formally adopt the CustomStringConvertible protocol. The CustomStringConvertible protocol requires that we implement a description String property; we do implement a description String property, so our code compiles. Now we can hand a Filter to print, or interpolate it into a string, and its description will appear automatically:
```swift
let type = Filter.albums
print(type) // Albums
print("It is \(type)") // It is Albums
```

### generic

Generic protocol with Self
In a protocol, use of the keyword Self (note the capitalization) turns the proto‐ col into a generic. Self is a placeholder meaning the type of the adopter. For example, here’s a Flier protocol that declares a method that takes a Self parame‐ ter:
        protocol Flier {
            func flockTogetherWith(_ f:Self)
}

### extension

An extension can’t override an existing member (but it can overload an existing method).

### inferring value:

```swift
class Color{
    var name:String = ""
    init(_ color:String){self.name = color}
}
extension Color{
    static var orange:Color {return Color("orange")}
    static var green:Color {return Color("green")}
    static var blue:Color {return Color("blue")}
}
func test(_ a:Color){
    Swift.print("Color: \(a.name)")
}
test(.orange)//orange
test(.blue)//blue
test(.green)//green
```

### Where clause:
An interesting problem arises when you want your generic extension where clause to specify type equality (==) instead of protocol adoption or class inheritance (:). The problem is that you can’t do that with a generic struct. Suppose, for example, that I want to give Array a sum method when the elements are Ints. I can’t do it:
```swift

    extension Array where Element == Int { // compile error
        func sum() -> Int {
            return self.reduce(0, +)
        }
}

```

But you can do it with a generic protocol, so the trick is to extend a generic protocol adopted by your struct. In this case, there is already a generic protocol adopted by Array, namely Sequence; so the solution is extend that instead:

```swift

    extension Sequence where Iterator.Element == Int {
        func sum() -> Int {
            return self.reduce(0, +)
        }
}
```