My notes on Infinite tree list<!--more-->  This could be rather simple actually. 

```swift
//Then you start designing Infinite treeList
    //differentiate indentation via css-classifier
        //you prob need classId for this, but use element-id for first interpolation
    //when you open an item, you basically insert items into a flatList 🚫
        //you set the css-classifer to the correct indentation 
    //when you hide children, you basically remove items from a flatList 🚫
    
    
//Basically you could Just use FastList with a treeList DP. 👍
    //if you click on an item open/close icon, you change the dp. and the dp changes FastList 👍
    //The TreeListDP will set the indentation by changing the css-selector 👍
```

- You also need to implement The side scroller. And make a sensible solution for Views that can scroll both ways. 
- Thinking about it, this will easily enable filtering the TreeList through search 👌

- FastList that can scroll x/y. basically you just scroll the contentContainer and render takes care of placing items in y
- You could also just move the items.x when x scroll is detected

```swift
//Tasks:
	//Make ElasticView again with v2 scrolling code 👈
		//make the ElasticView as small as possible
		//make call everything ...2 to differentiate (duplicate utils code if needed) 
	//Make List that can scroll both ways. 
	//Make fastList that can scroll both ways
		//the problem occurs when you want a sideScrolling list. I guess this can be toggled via bool flag.
			//The Container view doesnt need dir, only list needs dir. as containerview is x/y directional
	//Maybe all lists and all views need x/y sliders, you just disable them when there is enough views
		//Make the code foot print as small as possible
```