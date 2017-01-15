Some notes on .framework <!--more--> 

## NOTES:

- Apple claims that its best to use less than 6 .frameworks in your app. Or else compile time may suffer

## Resources:

- Make a framework of your swift files in a xcode project. And also add playground that can import the framework: [here](https://medium.com/@LogMaestro/adding-playgrounds-to-your-xcode-project-79d5ea0c7087#.q27u3w639) 
- Use the a .framework file in other projects by copying it: [here](https://www.youtube.com/watch?v=vChxJ_Nk6kI) 

## Access level:

Swift has three levels of access control. Use the following rules of thumb when creating your own frameworks:
- **Public**: for code called by the app or other frameworks, e.g., a custom view.
- **Internal**: for code used between functions and classes within the framework, e.g., custom layers in that view.
- **Fileprivate**: for code used within a single file, e.g., a helper function that computes layout heights.
- **Private**: for code used within an enclosing declaration, such as a single class block. Private code will not be visible to other blocks, such as extensions of that class, even in the same file, e.g., private variables, setters, or helper sub-functions.