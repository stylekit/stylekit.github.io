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

```swift

```

Even when there are only two states, an enum is often better than, say, a mere Bool, because the enum’s states have names. With a Bool, you have to know what true and false signify in a particular usage; with an enum, the name of the enum and the names of its cases tell you its significance. More‐ over, you can store extra information in an enum’s associated value or raw value; you can’t do that with a mere Bool.