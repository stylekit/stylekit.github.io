Notes on adding external .framework files to playground. <!--more--> 

## Using .framework in playground:

In order to use multiple .framework in playground you have to: 

1. Create a new xcode project

2. save the xcode project as a workspace

3. File -> new target -> Cocoa framework -> name the framework (FrameWork.framework)

4. add the .framework files to the folder of your xcode project

5. drag the .framework files into the project (set target membership to FrameWork.framework)

6. cmd + b (aka build)

7. add a playground to the workspace (select the project and cmd + n)

8. Add this to your playground: 


## Using nested .framework files in playground:

Usually .frameworks rely on other .frameworks to work. playground doesn't allow this out of the box.

1. file -> new project -> cocoa framework -> call it Child.framework -> cmd+b

2. file -> new project -> cocoa framework -> call it Parent.framework 

3. Copy the Child.framework into the project folder of: Parent.framework 

4. Drag the child.framework into xcode. 

5. the .child .framework in the parent .framework and 

6. In the Parent.framework project: cmd + b (aka build)

7. file -> new project -> Call it: "MyApp"

8. file -> new target -> cocoa framework -> Call it FrameWork.framework   

9. copy Child.framework and Parent.framework into the MyApp project folder

10. drag Child.framework and Parent.framework into the MyApp xcode project

11. add Child.framework and Parent.framework in: general -> "embedded binaries" 

12. cmd + b (aka build)

13. When you run an app you can import the framework with ``@testable import Parent`` and it will work 

14. cmd + n -> playground -> name it MyPlayground

15. in playground make sure you add: (the order of imports is important) 🔑

```swift
@testable import FrameWork//<--links your external .framework files
@testable import Child
@testable import Parent

Parent.myMethod()
```


```swift
@testable import FrameWork //<--links your external .framework files
@testable import ThirdPartyFrameWork

ThirdPartyFrameWork.test()//Output: hello world
```

