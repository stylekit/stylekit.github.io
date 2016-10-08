Caching css styles<!--more-->. So parsing .css files takes between 5-10seconds on a 4-core 2010 MacBook Pro. To make it faster one could re-write the css parsing engine that uses RegExp. Or even using a speedier opensource css parsing engine from someone else. But then quick fixes would be hard to do. Or adding new features etc. 

Another option was to cache the styles after they were rendered. And then if no .css file changed in the subsequent runs, the pre rendered cached styles would be used. 

To accomplish this a couple of things was needed: 

1. A way to get data from the rendered styles (Reflection)
2. A way to rebuild the styles from a storage (UnWrapping)
3. A way to check if any .css files had been modified since last run

So a Reflection library was built in swift. And an UnWrapping library. There were a few open-source project that could Reflect and UnWrap. But some would only work with structs and others wouldn't work with CGColor for instance. So Building new libraries was justified. Also Reflection and UnWrapping is pretty complicated with swift as it's a "statically-typed-language" and so there needs to be a level of custom code to quite a few classes. Unlike Dynamically-typed-languages were you can automate most of all reflection and unwrapping. 

The Reflection and UnWrapping library was written as an universal library that can work on any class. Some classes needs to have custom code to work and this can be accomplished through extensions: 

https://github.com/eonist/swift-utils