Figure out how to store css in style-manager with hash

Every element runs over every style added to the styleManager

So by hashing each style 

Also create a cache system where you store the last 20 queries: 

You would need to store each style selector in a separate hash id.

And then instead of looping over style.selectors you loop over elementQuerrySelectors and for each selector found you querry the hash id. This could potentially increase look-up-time because so many more lookups would happen. Maybe the cache is good enough

You could create a hash table based on the num of selectors in a style. Because if a style has more selctors than the element -> then its not within scope and will not be used. This way you can decrease lookup-time. 

And also the last element.selector must match the last element.selectors so we could create a hash table. The exception is the values that can inherit. (we could make a different system for these values)

A seperate array for styles that have inheritable values. and filtering values upon match.



**element selectors: **

```
Window Button#custom Text#buttonText
```

**Style Selector:**

```
Button Text (applies)
Window TextArea (does not apply)
Window (partly applies, font etc)
```


 
```swift
//cache idea (sudo code):
cache.recentlyUsed = []

//cache.style()

//you ask StyleResolver.style for the style. which has
//cache then queries the 10 last used styles it has in cache.styles
	//if cache.styles doesn't have the absolute style. 
		//style = StyleResolver.resolveStyle()
		//let idx = -1
		//for i < .count{
			//if($0.address == absolute-style-address){
				//idx = i
				//break
		//if(idx != -1)//already exists in cache
			ArrayModifier.indexSwap(.recentlyUsed,idx)//move to front
		//else//does not exist in cache
			//if(recentlyUsed.count > 9){
				//recently.popLast()
			//recently.unshift((style,address))//add to front
				

//let absolute-element-selector-address = ElementParser.stackString(button) 
//let address = SelectorParser.string($0.selectors)

```
The cache system should also move the most popular queries to the top of the array list
so basically the the cache styles should be like this -> cache.styles:[(IStyle,Int)] (<--using duplets where int is the popularity count) (popularity is good for repeating calls to styleResolver. like on hover etc)

```swift
StyleManger.getStyles(elementSelectors.count)

var maxSelectorCount:Int?
var minSelectorCount:Int?
var hashedStyles:Dictionary<selectorCount,[IStyle]>
//[]?
/*
 * NOTE: the hashedStyles are sorted on selectorCount from 1 and upwards
 */
func getStyles(selectorCount:Int)-> [IStyle]{
    var styles:[IStyle]
    for i = selectorCount; count < maxSelectorCount; i++;{
        if let value = hashedStyles[i.string]{
            styles += value
        }
    }
    return styles
}
```



- [x] build the recently queries cache system (its easy) 
- [ ] build the selector-count hashtable system (its easy too)
- [ ] build the cache system that is based on popularity
- [x] Test if speed goes up after implementing these two optimization efforts (use a timer before and after)
- [ ] More struct classes will speed things up probably. Style could be struct maybe? 
- [ ] Use Enum instead of constants?
- [ ] consider to build selector.last hashtable that would speed things up even further
- [ ] Figure out why copying values is faster than changing them. 