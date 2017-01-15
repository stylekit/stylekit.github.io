Notes on Swift package manager<!--more--> Swift package manager seems like the easier to use than CocoaPod and Carthage. Here is the basic workflow:

## Export: 
1. Add an empty Package.Swift to your xcode project
```swift
import PackageDescription
let package = Package(
  name: "Element"
)
```
2. keep all other .swift files you want to include in the package in a folder named Sources
3. Upload the Sources folder and the Package.swift file to github


## Import: 

1. add a Package.swift to your xcode project with example: 
```swift
import PackageDescription
let package = Package(
    name: "Element",
    dependencies: [
        .Package(url: "https://github.com/eonist/Element.git", majorVersion: 1),
    ]
)
```
2. navigate to the folder in terminal ``cd ~/Documents/dev/SomeProject/``
3. in terminal execute ``swift build``