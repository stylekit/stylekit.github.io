## Examples of singletons

```swift
class SingletonA {

    static let sharedInstance = SingletonA()

    init() {
        println("AAA");
    }

}


class TheOneAndOnlyKraken {
    static let sharedInstance = TheOneAndOnlyKraken()
    private init() {} //This prevents others from using the default '()' initializer for this class.
	func test(){
		print("hello world")
	}
}


let singleton = TheOneAndOnlyKraken.sharedInstance
singleton.test()
```