My notes on SPM + XCode + Nested frameworks<!--more--> 

## Pretext:

You want to develop an awesome app: Like a Hackernews reader app. You have a time budget of a weekend. Which forces you to priorities ruthlessly. You want to make some innovative GUI that stands out. Lots of nice animation via gestures etc. You need 3 frameworks to do it: Element for GUI awesomeness, AlamoFire for simple communication with hackernews.com. SwiftyJSON for parsing data from AlamoFire. Now you want to download these dependencies and build them in a way that a single person can work on it and a team. So you need your code to be on github. 

## Dependency map:
The chain of dependencies looks like this: Its only 2 level deep: (It can go deeper if needed)   
``[HackerNewsApp] -> [AlamoFire, SwiftyJSON, Element -> [swift-utils]]``

## Manifest: 

Inside your Package.swift file you write this:

```swift
import PackageDescription
let package = Package(
    name: "Testing",
	dependencies: [
		/*Downloads Element + swift-utils*/
		.Package(url: "https://github.com/eonist/Element.git", Version(0, 0, 0, prereleaseIdentifiers: ["alpha", "5"])),
		/*Downloads AlamoFire*/
		.Package(url: "https://github.com/Alamofire/Alamofire.git",MajorVersion:4,minor:3),
		/*Downloads SwiftyJSON*/
		.Package(url: "https://github.com/SwiftyJSON/SwiftyJSON.git",MajorVersion:3,minor:1)
    ]
)
```

## Workflow:

1. Terminal: ``cd dev/HackerNews``
2. Terminal: ``swift package init`` 👈 Creates boilerplace Package.swift etc
3. Replace the content inside HackerNews/Package.swift with the code written in the Manifest paragraph
4. Terminal: ``swift build`` 👈 Downloads and builds all the dependencies. 
5. Terminal: ``swift package generate-xcodeproj`` 👈 Creates HackerNews.xcodeproj
6. Follow this [Tutorial](http://stylekit.org/blog/2017/02/05/Xcode-and-spm/)  on how to Create an App project from this HackerNews.xcodeproj file
