Hot reloading in swift <!--more--> 

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


```swift
@testable import FrameWork //<--Import the framework first (links your external .framework files)
@testable import Element

let button:Button = Button()
addSubView(button)
```

