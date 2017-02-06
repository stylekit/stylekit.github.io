My notes on SPM + XCode + Nested frameworks<!--more--> 

## Pretext:

You want to develop an awesome app: Like a HackerNews reader app. You have a time budget of a weekend. Which forces you to priorities ruthlessly. You want to make some innovative GUI that stands out. Lots of nice animation via gestures etc. You need 3 frameworks to do it: Element for GUI awesomeness, AlamoFire for simple communication with hackernews.com. SwiftyJSON for parsing data from AlamoFire. Now you want to download these dependencies and build them in a way that a single person can work on it and a team. So you need your code to be on github. 

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
7. Once you have your first "Hello world" going. Start adding some innovative UX ideas to your App project. 
8. Need to update dependencies or add new ones? Just edit your Package.swift file and Terminal: ``swift build`` 
9. To add your app project to Github all you do is make a new project on github.com and add a .gitignore file that ignores /.build, /Tests,/ Packages and .xcodeproj. Then you can stay in-sync with other team-members etc. 

## Final word:  
I would love to include some HackNewsApp Example code. And I plan to. Until then you have to figure out how to use AlamoFire, Element and SwiftyJSON your self. At least now you have a solid foundation of how to start making Apps with SPM.