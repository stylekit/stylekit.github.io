My notes on CI travis<!--more--> 


## Notes:

- Comments can be written as #

A typical .yml file looks like this:
```yml
os:
  - osx
language: generic
sudo: required
dist: trusty
osx_image: xcode8
script:
  - swift build
#  - swift test
notifications:
  email:
    on_success: never
    on_failure: change
```