SPM + XCode tutorial<!--more--> 

## Prextext:
Here is how you use SPM in your app projects. SPM -> Swift package manager 

## The workflow:  

1. Terminal: ``cd ~/dev/MyProject/`` 👈 navigate to your project
2. Terminal: ``swift package init`` 👈 creates the initial SPM files  
3. Add the bellow to your newly created Package.swift files: 
```swift
import PackageDescription
let package = Package(
    name: "MyProject",
	dependencies: [
		.Package(url: "https://github.com/eonist/swift-utils.git", Version(0, 0, 0, prereleaseIdentifiers: ["alpha", "3"]))
    ]
)
```
👆 basically adds Swift-utils as a third Party framework in your project  

4. Terminal: ``swift build`` 👈 downloads the dependencies from github and builds binaries (aka .framework)  
5. Terminal: ``swift package generate-xcodeproj`` 👈  Creates an XCode project that has .framework files
6. XCode: Open the .xcodeproj file file -> Target -> Cocoa app
7. XCode: Add this: add ``@testable import Utils`` to ``AppDelegate.swift`` and ``print(StringParser.sansSuffix("blue"))`` inside the ``applicationDidFinishLaunching`` method
8. ``cmd + r`` will now print ``blu``
