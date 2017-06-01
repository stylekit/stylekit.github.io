The phrase: Build something simple. You can always customize and add features later. That got me thinking 🤔. What if we combine JSON and FlexBox with Element. Here is my idea:

1. You write the app structure in JSON. 
2. Then you add some CSS that use flexbox to position the layout. 
3. Then you add some event handling swift code that reacts to interaction

Test your app: Does it resize correctly, how does it look in fullscreen, dark mode look good? 👌

#### SWIFT:
```swift

self.onEvent{ event in
	if event.type == .buttonClick && event.immediate == "commitPrompt" && event.origin.id == "ok" {
		/*Add commit logic here*/
		Nav.view = Nav.previous/*transition back after commit completes*/
	}else if event.type == .select && event.immediate == "repo" {
		Nav.view = Nav.getView("repoDetail")
		let idx:[Int] = event.index
		/*Call a method that sets the UI components to the data at idx in repos.JSON*/
	}else if event.type == .swipeRight && event.immediate.id == "repoDetail"{
		/*Call method that collects data from UI and overrides the JSON element*/
		Nav.view = Nav.getView("repo")/*Transition back to repo*/
	}
}

This is just 1 event Handler for the entire App to test it quickly. This isn't sustainable in the long run as you build out the app. You can extract the event Logic into other methods. Or subclass the Views. I.e: `RepoView` you then specify to use this class in the JSON. 

```
#### CSS:
```

```
//add json for the Menu system as well. and add some basic events for it in swift. Fullscreen, darkmode
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
			content:[
				RepoList:{
					id:repoList,
					itemHeight:24
				}
			]
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
			id:"prefs",
			content:{
				TextInput:{id:login,text:"github-user"}
				TextInput:{id:pass,text:"github-password"}
				CheckBoxTextButton:{id:dark,text:"Dark-mode",checked:false}
			}
		}
		View:{
			id:errorPromt,
			content:[
				Text:{id:title,text:"There was an error"}
				Container:{
					id:"confirm",
					content:{
						TextButton:{id:ok},
						TextButton:{id:cancel}
					}
				}
			]
		}
		View:{
			id:commitPrompt,
			content:[
				Text:{id:title,text:"Commit changes"},
				TextArea:{id:msg},
				Container:{
					id:"confirm",
					content:{
						TextButton:{id:ok},
						TextButton:{id:cancel}
					}
				}
			]
		}
		View:{
			id:MergePrompt,
			content:[
				Text:{id:desc},
				RadioGroup:[
					RadioButtonButton:{id:local,title:"Use local file"},
					RadioButtonButton:{id:remote,title:"Use remote file"},
					RadioButtonButton:{id:remote,title:"Use mix of both"}
				],
				Container:{
					id:"confirm",
					content:{
						TextButton:{id:ok},
						TextButton:{id:cancel}
					}
				}
			]
		}
	}
}
```


**End-note:**
Customization is key to creating an artisan experience. But customization should not get in the way of DRY: Don't repeat your self. If you have too much customization you can't easily iterate on the underlying code. Abstraction allows you to only focus on the logic of the app. 