Migration insights <!--more--> 


## Range
Range in swift 3 has been totally re-designed. 🙈

## For-loop

The one c-style for-loop to rule them all is gone, now we have 7 different to take its place: 

- ``for i in 0..4{}`` 👈 regular forward looping
- ``for (i,obj) in arr.enumerate(){print(i);print(obj)}`` 👈 access to i and obj
- ``for obj in arr{}`` 👈 iterate over objects
- ``for (i in 0..<4).reversed{}`` 👈 backward looping
- ``var i = 0;while(i<4){print(i);i+=1}`` 👈 If you want to manipulate i while looping
- ``for i in stride(from:0,to:10,skip:2){}`` 👈 Skips every other
- ``arr.forEach{$0}`` 👈 Easiest for-loop but only if you don't need to exit early

## NSView

``drawLayer(layer:CALayer, inContext ctx: CGContext)`` 👈 This has vanished with out a trace to work around build it your self. 
``actionForLayer(layer:CALayer, forKey event: String) -> CAAction?`` 👈 Also gone, Solution: build it your self.