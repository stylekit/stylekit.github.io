Notes on adding external .framework files to playground. <!--more--> 

## Using .framework in playground:

In order to use multiple .framework in playground you have to: 

1. Create a new xcode project

2. Save the xcode project as a workspace

3. Add a playground to the workspace (select the project and cmd + n) 

4. Name it MyPlayground and set the group to the workspace. 🔑

5. File -> new target -> Cocoa framework -> name the framework (FrameWork.framework)

6. add the .framework files to the folder of your xcode project

7. Drag the .framework files into the project (set target membership to FrameWork.framework)

8. cmd + b (aka build)



8. Add this to your playground: 

```swift
@testable import FrameWork //<--links your external .framework files
@testable import ThirdPartyFrameWork

ThirdPartyFrameWork.test()//Output: hello world
```


## Using nested .framework files in playground:

Usually .frameworks rely on other .frameworks to work. playground doesn't allow this out of the box.

1. file -> new project -> cocoa framework -> call it Child.framework -> cmd+b

2. file -> new project -> cocoa framework -> call it Parent.framework 

3. Copy the Child.framework into the project folder of: Parent.framework 

4. Drag the child.framework into XCode where you have the Parent XCode project

5. In the Parent.framework project: cmd + b (aka build)

6. file -> new project -> Call it: "MyApp"

7. file -> new target -> cocoa framework -> Call it FrameWork.framework   

8. Copy Child.framework and Parent.framework into the MyApp project folder

9. Drag Child.framework and Parent.framework into the MyApp xcode project

10. add Child.framework and Parent.framework in: general -> "embedded binaries" 

11. cmd + b (aka build)

12. When you run an app you can import the framework with ``@testable import Parent`` and it will work 

13. cmd + n -> playground -> name it MyPlayground

14. In playground make sure you add: (the order of imports is important) 🔑

```swift
@testable import FrameWork//<--links your external .framework files
@testable import Child
@testable import Parent

Parent.myMethod()//hello parent, hello child
```

## Final notes:

- Having the ability add frameworks to XCode is key to low build times and is also the only way to add external code to playground.  
- Being able to nest frameworks is a must when using Third Party FrameWorks and your own frameworks. 
- The workflow to get nested frameworks to work in playground is not optimal. **An alternative** is to compile all libraries as a single .framework. This can be done by creating empty .framework files so that the import statements doesn't complain. They need to be empty so that the compiler doesn't complain about duplicate classes. The final step is to copy the third-party framework .swift files into your project. Then follow the steps in "Using framework in playground"