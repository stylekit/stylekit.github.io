Drop this code into any subclass of NSView, to enable the hand cursor<!--more--> :  
```swift 
override func resetCursorRects() {
   let cursor:NSCursor = NSCursor.pointingHandCursor()
   addCursorRect(frame, cursor: cursor)
   cursor.setOnMouseEntered(true)
}
```
<img width="320" alt="img" src="https://dl.dropboxusercontent.com/u/2559476/Screen Shot 2015-11-21 at 19.48.08.png">
