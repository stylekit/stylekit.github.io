Notes on Swift package manager<!--more--> Swift package manager seems like the easier to use than CocoaPod and Carthage. Here is the basic workflow:

## Pretext:  
We are all DevOps now. There is no getting around this, if you want to code efficiently you have to master the art of DevOps. Or descend into "dependency hell". Package Dependency managers Are not easy to use, but one cannot live with out them. developing for apple devices requires you to use either Cocoapod Carthage or SPM. Which can be divided into 3 camps: The past, the present and the future. SPM being the future. 

## First impression using SPM:

SPM seems like a command-line tool for downloading projects that contain .swift files from github. It's able to derive files based on "Sem-Ver" tagging of committed code. I think it also supports nested dependencies but I haven't tested that part. And thats pretty much it. Which leaves a lot to be desired. Like support for binaries (.framework)? Which is really important when dealing with third-party libs. (binaries are a lot faster to compile that source code)

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

1. Add a Package.swift to your xcode project with example: 
```swift
import PackageDescription
let package = Package(
    name: "Element",
    dependencies: [
        .Package(url: "https://github.com/eonist/Element.git", majorVersion: 1),
    ]
)
```

Pick versions with this syntax: ``majorVersion: 0, minor: 4`` For more specific version picking use: ``Version(0, 0, 0, prereleaseIdentifiers: ["alpha", "3"])`` which would download ``0.0.0-alpha.3`` for ranges you can use syntax such as : ``Version(2, 0, 1) ..< Version(2, 1, 0)``



2. navigate to the folder in terminal ``cd ~/Documents/dev/SomeProject``
3. in terminal execute ``swift build``

## Excluding non-source files:  
Use this property to exclude files and directories from the package sources.  
```swift
let package = Package(
    name: "Foo",
    exclude: ["Sources/Fixtures", "Sources/readme.md", "Tests/FooTests/images"]
)
```

## Create .xcodeproj file via terminal:
cd to the respected folder
```bash
swift package generate-xcodeproj
```

## SPM dependency resolvent: 

If two packages depend on different versions of a third package, the package manager tries to find a version of that package that both will find acceptable.

## Drawbacks:

1. Unable to target Commit ids. Only release tags are supported. Which makes it difficult to have a fast workflow when evolving your projects. Releases should be significant and not iterate on every new commit. If you have a lot of nested frameworks which you should because modularity is good and thats why we have dependency managers in the first place. Apple has no intention to support targeting commit ids according to their mailing-list on SPM. Carthage has support for targeting commit ids and even ``"HEAD"`` However pushing a release tag isn't that much work but it is inconvenient. 