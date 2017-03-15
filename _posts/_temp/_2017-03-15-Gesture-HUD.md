

```swift
class TestView:NSView(){
    var gestureHUD:GestureHUD?
    init(){
        gestureHUD = GestureHUD(self)
        self.acceptsTouchEvents = true/*Enables gestures*/
        self.wantsRestingTouches = true/*Makes sure all touches are registered. Doesn't register when used in playground*/
    }
    override func touchesBegan(with event:NSEvent) {
        gestureHUD!.touchesBegan(event)
    }
    override func touchesMoved(with event:NSEvent) {
        gestureHUD!.touchesMoved(event)
    }
    override func touchesEnded(with event:NSEvent) {
        gestureHUD!.touchesEnded(event)
    }
}
```