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