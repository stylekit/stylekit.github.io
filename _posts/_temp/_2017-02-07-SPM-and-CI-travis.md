My notes on Swift PM + CI Travis<!--more--> 

## Workflow:

1. Terminal: ``cd dev/HelloTravis`` 👈 Navigate to a folder
2. Terminal: ``swift package init --type=library`` 👈 creates a testable setup
3. Terminal: ``swift test`` 👈 Runs the first test
4. add an .travis.yml see [YML paragraph](#yml) 

## YML

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