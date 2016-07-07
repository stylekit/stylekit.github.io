## **CALayer and implicit animation**
The animation was left in intentionally for this test. <!--more--> Animation won't be apart of Element yet.   
<img width="240" alt="img" src="https://dl.dropboxusercontent.com/u/2559476/2f289u9384f34.gif">

## **Stop implicit animation on a layer in swift:**
```swift
override func actionForLayer(layer: CALayer, forKey event: String) -> CAAction? {
    return NSNull()
}
```
Remember to set the delegate of your CALayer instance to an instance of a class that at least extends NSObject. In this example we extend NSView.
