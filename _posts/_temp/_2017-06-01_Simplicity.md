Build something simple. You can always customize and add features later. That got me thinking 🤔. What if we combine JSON and FlexBox with Element. Here is my idea:

1. You write the app structure in JSON. 
2. Then you add some CSS that use flexbox to position the layout. 
3. Then you add some event handling swift code that reacts to interaction

Test your app: Does it resize correctly, how does it look in fullscreen, dark mode look good? 👌

#### SWIFT:
```swift

self.onEvent{ event in
	if event.type == .buttonClick && event.origin.id == "ok" {
		/*Add commit logic here*/
		Nav.view = Nav.previous/*transition back after commit completes*/
	}else if event.type == .select && event.immediate(where:{$0.id == "repoList"}) {
		Nav.view = Nav.getView("repoDetail")
		let idx:[Int] = event.index
		/*Call a method that sets the UI components to the data at idx in repos.JSON*/
	}else if event.type == .swipeRight && event.immediate.id == "repoDetail"{
		Nav.view = Nav.getView("repo")/*Transition back to repo*/
	}
}
```
#### CSS:
```

```
#### JSON:
```
{
	title:GitSync,
	size:{w:400,h:600},
	min-size:{w:300,h:300},
	max-size:{w:600,h:1000},
	pages:{
		View:{
			id:repo,
			content:{
				RepoList:{
					id:repoList,
					itemHeight:24
				}
			}
		},
		View:{
			id:repoDetail,
			content:{
				TextInput:{id:name,text:Name},
				TextInput:{id:local,text:Local-path},
				TextInput:{id:remote,text:Remote-path},
				TextInput:{id:branch,text:Branch},
				CheckBoxTextButton:{id:auto,text:Auto,checked:false}
			}
		},
		View:{
			id:commitPrompt,
			content:{
				Text:{id:title},
				TextArea:{id:msg},
				TextButton:{id:ok},
				TextButton:{id:cancel}
			}
		}
	}
}
```


**End-note:**
Customization is key to creating a artisan experience. But customization should not get in the way of DRY: Don't repeat your self. If you have too much customization you can really iterate on the underlying code. Abstraction allows you to only focus on the logic of the app. 