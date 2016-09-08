Figure out how to store css in style-manager with hash

Every element runs over every style added to the styleManager

So by hashing each style 

Also create a cache system where you store the last 20 queries: 

You would need to store each style selector in a separate hash id.

And then instead of looping over style.selectors you loop over elementQuerrySelectors and for each selector found you querry the hash id. This could potentially increase look-up-time because so many more lookups would happen. Maybe the cache is good enough

You could create a hash table based on the num of selectors in a style. Because if a style has more selctors than the element -> then its not within scope and will not be used. This way you can decrease lookup-time. 

And also the last element.selector must match the last element.selectors so we could create a hash table. The exception is the values that can inherit. (we could make a different system for these values)



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
let absolute-element-selector-address = ElementParser.stackString(button) 
if (cache.styles.count > 0) {
	cache.styles.forEach{
		if(absolute-element-selector-address == SelectorParser.string($0.selectors)){
			return $0
		}
	}
}
```
The cache system should also move the most popular queries to the top of the array list
so basically the the cache styles should be like this -> cache.styles:[(IStyle,Int)] (<--using duplets where int is the popularity count)


- [ ] build the cache system
- [ ] build the selector-count hashtable system
- [ ] Test if speed goes up after implementing these two optimization efforts
- [ ] More struct classes will speed things up probably. Style could be struct maybe? 
- [ ] Use Enum instead of constants?