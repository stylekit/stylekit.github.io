spend zero time managing dependencies <!--more-->Build speed is almost down to zero even for big projects, and 99.99% of my time i spent actually coding. 


## Wants: 

1. Ability to Build from .framework (because of zero to low build times) ✅
2. Syncronize source code across projects autonomously (many to many sync) ✅
3. Syncronize directly to 1 singular ~~mothership~~ origin repo at github (version control) ✅
4. Full SPM integration (Sharing code) ✅
5. Ability to edit external framework code directly inside app projects, and automatically sync back to origin. ✅
6. Playground friendly (since you are building .frameworks it works in playground) ✅
7. iOS support  (macOS only, Apple is working on iOS support, Nightly builds should have this) 🚫
  
To achieve this: read my series on SPM (Swift package manager) and use [GitSync](http://www.gitsync.io)   

## SPM Series:  
- [Faster xcode with spm](http://stylekit.org/blog/2017/02/10/Faster-XCode-with-SPM/) 
- [Spm and ci travis](http://stylekit.org/blog/2017/02/07/SPM-and-CI-travis/) 
- [Spm and nested frameworks](http://stylekit.org/blog/2017/02/06/SPM-and-nested-frameworks/)
- [Xcode and spm](http://stylekit.org/blog/2017/02/05/Xcode-and-spm/) 

## Scenario:

**Problem:**  
You have a Testing xcode project, A Library xcode project and an App xcode project. You want to fix a problem in your Library. And you want to test if the fix works, if it does you want to see that change in the app project. 
  
**Solution:**  
This would require an enormous amount of work to achieve. Even the simplest variable change would take 15 minutes to propagate and be perfectly aligned in all projects and git repos etc etc. All this is automatic with GitSync + SPM. You simply change the lib hit cmd save in xcode and all the other projects are synced within seconds. Just switch tab and see the changes be reflected. Then just run your test and your app and .frameworks will be rebuilt and source is up today. Thats not all. You don't have to edit your code in your test library. You can edit the lib code right in your app code. GitSync syncs uni-directionally. 