Reducing for-loops is a great way to maintain readability and maintain code modularity. Methods like map, flatMap, filter and reduce are awesome building blocks for functional programing in swift, but you can also build your own custom methods that do similar things. <!--more--> Here is a trick were we use closure blocks to encapsulate the method call. The for loop is the same but the method call is different. This approach is great when you need the code within the for-loop to be the same but you want to have the code within different methods to be different. 

```swift
import Foundation

class Brick{
    var active:Bool
    var focused:Bool
    var name:String
    init(_ active:Bool,_ focused:Bool, _ name:String){
        self.active = active
        self.focused = focused
        self.name = name
    }
    func isActive()->Bool{
        return active
    }
    func isFocused()->Bool{
        return focused
    }
}
private class Utils{
    /**
     *
     */
    static func performAction(bricks:Array<Brick>, _ action:(Brick)->Bool)->Brick?{
        for brick in bricks{
            if(action(brick)){
				return brick
			}
        }
        return nil
    }
}

let a:Brick = Brick(true,false,"a")
let b:Brick = Brick(false,true,"b")
let c:Brick = Brick(true,true,"c")
let bricks = [a,b,c]

print(Utils.performAction(bricks, {$0.isActive()})!.name)//a
print(Utils.performAction(bricks, {$0.isFocused()})!.name)//b
```