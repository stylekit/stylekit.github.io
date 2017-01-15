Notes on Swift package manager<!--more--> 

## Export: 
1. Add an empty Package.Swift to your xcode project
```swift
import PackageDescription
let package = Package(
  name: "Element"
)
```
2. Upload your project to github (the requirements for what files to include are unknown at this time)

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