```swift
/**
 * Detects when touches are made
 * NOTE: event.localPos(self) equals the pos of the mouseCursor
 */
override func touchesBegan(with event:NSEvent) {
    //Swift.print("touchesBeganWithEvent: " + "\(event)")
    /*Debug*/
    gestureHUD!.touchesBegan(event)
}
/**
 * Detects if a two finger left or right swipe has occured
 */
override func touchesMoved(with event:NSEvent) {
    //Swift.print("touchesMovedWithEvent: " + "\(event)")
    /*Debug*/
    gestureHUD!.touchesMoved(event)
}
/**
 * NOTE: playground doesn't fire a touch up when there is only one touch detected. to work aroudn this limitation you have to detect any touch and then when there are only 2, delete all debugCircs
 */
override func touchesEnded(with event:NSEvent) {//for debugging
    Swift.print("touchesEndedWithEvent: " + "\(event)")
    //Swift.print("event.phase.type: " + "\(event.phase.type)" + " event.phase: " + "\(event.phase)")
    /*Debug*/
    gestureHUD!.touchesEnded(event)
}
override func touchesCancelled(with event:NSEvent) {//for debugging
    Swift.print("touchesCancelledWithEvent: " + "\(event)")
}
```