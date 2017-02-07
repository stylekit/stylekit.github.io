My notes on Swift PM + CI Travis<!--more--> 

## Workflow:

1. Create a project named HelloTravis on github. Then download it via Github desktop app
2. Terminal: ``cd dev/HelloTravis`` 👈 Navigate to the folder you just downloaded
3. Terminal: ``swift package init --type=library`` 👈 creates a testable setup
4. Terminal: ``swift test`` 👈 Runs the first test
5. add an .travis.yml see [YML paragraph](#yml) 
6. Uploaded all the changes to github again. 
7. Create an account at: [travis-ci.org](https://travis-ci.org) (it takes zero time if you are logged into github)
8. Find your HelloTravis project in your account list. Then switch the on/off but to on. 
9. Copy the MarkDown badge and add it to your README.md file in the HelloTravis project on github. 
10. Wait a little while and your Badge will become Green if all tests pass. 
11. Add More complex tests under the HelloTravis/Tests/HelloTravisTests.swift file. 
12. Add nested dependencies to your Tests via my [Tutorial on SPM + Nested tests](http://stylekit.org/blog/2017/02/06/SPM-and-nested-frameworks/) 

## bash

A typical .yml file looks like this: 
```yml
os:
  - osx
language: generic
sudo: required
dist: trusty
osx_image: xcode8.2
script:
  - swift build #Builds the dependencies
  - swift test #Tests whatever is inside the Test folder
notifications:
  email:
    on_success: never
    on_failure: change
```

## Final word: 

Since you have to create a special library package to enable 