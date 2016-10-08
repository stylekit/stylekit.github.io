parsing .css files takes between 5-10secs on a 4-core 2013 MacBook Pro Retina. To make it faster <!--more--> one could re-write the css parsing engine that uses RegExp. Or even using a speedier open-source css parsing engine from someone else. But then quick fixes would be hard to do. Or adding new features etc.   

Another option was to cache the styles after they were rendered. And then if no .css file changed in the subsequent runs, the pre rendered cached styles would be used. The result of the optimization efforts proved to be worthwhile. The loading of A window packed with GUI elements now loads bellow 1 sec. Which really is imperceptible. Loading regular interfaces will be near instant. 

## To accomplish this a couple of things was needed: 

1. Get data from the rendered styles (Reflection)  
2. Rebuild the styles from a storage (UnWrapping)  
3. Check if any .css files had been modified since last run  

So a Reflection library was built in swift. And an UnWrapping library. There were a few open-source project that could Reflect and UnWrap. But some would only work with structs and others wouldn't work with CGColor for instance. So Building new libraries was justified. Also Reflection and UnWrapping is pretty complicated with swift as it's a "statically-typed-language" and so there needs to be a level of custom code to quite a few classes. Unlike Dynamically-typed-languages were you can automate most of all reflection and unwrapping.   

The Reflection and UnWrapping library was written as an universal library that can work on any class. Some classes needs to have custom code to work and this can be accomplished through extensions: 

## Reflection and UnWrapping Example code:

```swift
/**
 * NOTE: we use 32 bit RGBA values when storing color data (This also stores the alpha value)
 * NOTE: XML is used as the storage syntax. JSON could be used but there was no apparent benefit so XML it is
 */
let temp = Temp(NSColor.redColor())
let xml = Reflection.toXML(temp)/*Reflection*/
print(xml.XMLString)//Output: <Temp><color type="NSColor">FFFF0000</color></Temp>
let newInstance = Temp.unWrap(xml)!/*UnWrapping*/
print(newInstance.color.hexString)//Output: FF0000

class Temp{
    var color:NSColor
    init(_ color:NSColor){
        self.color = color
    }
}
extension Temp:UnWrappable{
    static func unWrap<T>(xml:XML) -> T? {
        let color:NSColor? = unWrap(xml,"color")
        return Temp(color!) as? T
    }
}

```

The Reflection and UnWrapping library can be found here: https://github.com/eonist/swift-utils