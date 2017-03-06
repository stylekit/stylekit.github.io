Explains how one could do **"upstream-event-propagation"** and **"downstream-state-distribution"**:<!--more--> 

<img width="680" alt="img" src="https://rawgit.com/stylekit/img/master/event_and_state_diagram.svg">

**In Element we don't distribute state**. State is derived by asking up hierarchy about the entire "hierarchy-state" and then calculating final state for the descendants.  We still have to distribute the state call to call the render() recursively to each descendant. But we don't pass an externalState down hierarchy. The passing of externalState down hierarchy example described in the diagram is to enable state change in AppKit since AppKit doesn't do the whole CSS thing that Element does and cant look up hierarchy to derive its design.

In element we would rather do:
```css
/*All Buttons that descend from window will now use the white fill and grey line when window is set to inactive*/
Window :inactive Button{
   fill:white;
   line:grey;
}
```

And thats all the code thats needed to add an inactive mode for all Buttons in Window. 

If we need more granularity: We do: 

```css
Window :inactive TitleBar Button{
   ...
}
```

Now only buttons inside**TitleBar** inside **Window** gets this inactive look. 
And other buttons render in a default style.
