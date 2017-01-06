An overview of how Element works: <!--more--> 



<img width="440" alt="img" src="https://raw.githubusercontent.com/stylekit/img/master/Element_parts.png">

- Every GUI component has 1 Element
- Element has 3 parts: Skin, Style and State


## Skin:

There are 2 types of Skin types: GraphicsSkin and TextSkin

<img width="364" alt="img" src="https://raw.githubusercontent.com/stylekit/img/master/skin_types.png">

There 2 Skin types: GraphicSkin and TextSkin

<img width="312" alt="img" src="https://raw.githubusercontent.com/stylekit/img/master/graphic_types.png">

GraphicSkin has multiple layers of Graphic layers More info about the graphic rendering system [here](http://stylekit.org/blog/2015/12/30/Graphic-framework-for-OSX/) 

<img width="350" alt="img" src="https://raw.githubusercontent.com/stylekit/img/master/skin_layers.png">

<img width="298" alt="img" src="https://raw.githubusercontent.com/stylekit/img/master/graphics_parts.png">


By dividing the graphics into two parts we can independently update the design. 

## State:

The state is just a string that changes over time when the user interacts with the Element. Can be overDownCheckedFocused etc. then the Element is styled accordingly, by looking for a style that matches this combination of states.

<img width="264" alt="img" src="https://raw.githubusercontent.com/stylekit/img/master/state_types.png">