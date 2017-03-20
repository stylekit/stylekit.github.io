<!--more--> 


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

### Type assertion:

```swift
 func typeTester(_ d:Dog, _ whattype:Dog.Type) {
        if type(of:d) === whattype {
// ... }
}
```

### Array tricks tricks

An array also has an initializer whose parameter is a sequence. This means that if a type is a sequence, you can split an instance of it into the elements of an array. For example:
• Array(1...3) generates the array of Int [1,2,3].
• Array("hey".characters) generates the array of Character ["h","e","y"].
• Array(d), where d is a Dictionary, generates an array of tuples of the key–value pairs of d.


### Array slicing

An array’s largest accessible index is one less than its count. You may find yourself calculating index values with reference to the count; for example, to refer to the last two elements of arr, you can say:
```swift
let arr = [1,2,3]
let slice = arr[arr.count-2...arr.count-1] // [2,3]
```
Swift doesn’t adopt the modern convention of letting you use negative numbers as a shorthand for that calculation. On the other hand, for the common case where you want the last n elements of an array, you can use the suffix(:) method:
```swift
let arr = [1,2,3]
let slice = arr.suffix(2) // [2,3]
```
Both suffix(:) and its companion prefix(:) yield ArraySlices, and have the remarkable feature that there is no penalty for going out of range:
```swift
let arr = [1,2,3]
let slice = arr.suffix(10) // [1,2,3] (and no crash)
```
Instead of describing the size of the suffix or prefix by its count, you can express the limit of the suffix or prefix by its index:
```swift
let arr = [1,2,3]
let slice = arr.suffix(from:1)    // [2,3]
let slice2 = arr.prefix(upTo:1)    // [1]
let slice3 = arr.prefix(through:1) // [1,2]

```
    
### array idx

The index(of:) method reports the index of the first occurrence of an element in an array, but it is wrapped in an Optional so that nil can be returned if the element doesn’t appear in the array. If the array consists of Equatables, the comparison uses == behind the scenes to identify the element being sought:
```swift
let arr = [1,2,3]
let ix = arr.index(of:2) // Optional wrapping 1
```
Alternatively, you can call index(where:), supplying your own function that takes an element type and returns a Bool, and you’ll get back the index of the first element for which that Bool is true. In this example, my Bird struct has a name String property:
```swift
let aviary = [Bird(name:"Tweety"), Bird(name:"Flappy"), Bird(name:"Lady")]
let ix = aviary.index {$0.name.characters.count < 5} // Optional(2)
```
    
Array sequence

As a sequence, an array’s contains(:) method reports whether it contains an ele‐ ment. Again, you can rely on the == operator if the elements are Equatables, or you can supply your own function that takes an element type and returns a Bool:
```swift
let arr = [1,2,3]
let ok = arr.contains(2) // true
let ok2 = arr.contains {$0 > 3} // false
```
The starts(with:) method reports whether an array’s starting elements match the elements of a given sequence of the same type. Once more, you can rely on the == operator for Equatables, or you can supply a function that takes two values of the ele‐ ment type and returns a Bool stating whether they match:
```swift
let arr = [1,2,3]
let ok = arr.starts(with:[1,2]) // true
let ok2 = arr.starts(with:[1,-2]) {abs($0) == abs($1)} // true
```    
The elementsEqual(:) method is the sequence generalization of array comparison: the two sequences must be of the same length, and either their elements must be Equatables or you can supply a matching function


### Array joined

The joined(separator:) instance method starts with an array of arrays. It extracts their individual elements, and interposes between each sequence of extracted ele‐ ments the elements of the separator:. The result is an intermediate sequence called a JoinSequence, and might have to be coerced further to an Array if that’s what you were after. For example:
```swift
let arr = [[1,2], [3,4], [5,6]]
let joined = Array(arr.joined(separator:[10,11]))
// [1, 2, 10, 11, 3, 4, 10, 11, 5, 6]
```
Calling joined() with no separator: is a way to flatten an array of arrays. Again, it returns an intermediate sequence (or collection), so you might want to coerce to an Array:
```swift
let arr = [[1,2], [3,4], [5,6]]
let arr2 = Array(arr.flatten())
// [1, 2, 3, 4, 5, 6]
```
    
Array sort

```swift
arr.sort {$0 > $1} // [6, 5, 4, 3, 2, 1]
```

### Dictionary:

You can extract a dictionary’s entire contents at once as an array (of key–value tuples) by coercing the dictionary to an array:
```swift
var d = ["CA": "California", "NY": "New York"]
let arr = Array(d) // [("NY", "New York"), ("CA", "California")]
```


##Set


A set (Set, a struct) is an unordered collection of unique objects. Its elements must be all of one type; it has a count and an isEmpty property; it can be initialized from any sequence; you can cycle through its elements with for...in. But the order of ele‐ ments is not guaranteed, and you should make no assumptions about it.
The uniqueness of set elements is implemented by constraining their type to be Equatable and Hashable, just like the keys of a Dictionary. Thus, the hash values can be used behind the scenes for rapid access. Checking whether a set contains a given element, which you can do with the contains(_:) instance method, is very efficient — far more efficient than doing the same thing with an array. Therefore, if element uniqueness is acceptable (or desirable) and you don’t need indexing or a guaranteed order, a set can be a much better choice of collection than an array.