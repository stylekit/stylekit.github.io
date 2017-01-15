Some notes on .framework <!--more--> 

### NOTES:

- Apple claims that its best to use less than 6 .frameworks in your app. Or else compile time may suffer

### Resources:

- Make a framework of your swift files in a xcode project. And also add playground that can import the framework: [here](https://medium.com/@LogMaestro/adding-playgrounds-to-your-xcode-project-79d5ea0c7087#.q27u3w639) 
- Use the a .framework file in other projects by copying it: [here](https://www.youtube.com/watch?v=vChxJ_Nk6kI) 
- Export and Drag and drop .framework to different projects: [here](http://stackoverflow.com/a/40991398/5389500) 
- Nice video [here](https://realm.io/news/tryswift-jeff-hui-creating-a-swift-library/) 
### Access level:

Swift has three levels of access control. Use the following rules of thumb when creating your own frameworks:
- **Public**: for code called by the app or other frameworks, e.g., a custom view.
- **Internal**: for code used between functions and classes within the framework, e.g., custom layers in that view.
- **Fileprivate**: for code used within a single file, e.g., a helper function that computes layout heights.
- **Private**: for code used within an enclosing declaration, such as a single class block. Private code will not be visible to other blocks, such as extensions of that class, even in the same file, e.g., private variables, setters, or helper sub-functions.

### Export / Import:

1. Right click on the ‘MotionKit.framework’ and select ‘Show in Finder’
 
2. Now click and drag this .framework file into any of the projects that you want. In my case, I’d drag into my own project,

3. In your new project: Project settings -> General -> Embedded bins and Linked frameworks / libs -> add the  .framework via the + button

