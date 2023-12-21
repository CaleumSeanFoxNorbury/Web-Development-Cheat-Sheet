# Ionic With Cordova

## Index

...

## SetUp 

...

## Introduction 

Cross-Platform integration framework, Ionic creates a suitable environment for native applications. 

After downloading Ionic CLI package, we can create a new ionic application usin the following command - `ionic start`.

...

## Builds 

### Browser

Browser builds with cordova can work however Ionic is meant for more native builds like `android` or `ios`. 

***Issue***

SQLite is not meant for non-native builds and isnt compatible within the browser - Reference #002

Reference #001

***Work Around***

Using Ionic storage, we are able to store our data securly and is compatible with browser builds - Reference #003. 

## IOS 

IOS builds can be easily configured and ran out for any Apple devices and work well for consdierations and requirements for their application store.

***Tips***

### IOS Simulator

This simulator allows testing and debugging before the application actually reachers a device. This simulator requires XCode and Apples IDE to be installed and then the application can emulator around the mentioned simulator.

`ionic cordova emulate ios -lc`

- `-lc` - enables livereload and console outputs to the terminal or logcast

## Android

...

## Reference

- SQLite Browser Issue https://stackoverflow.com/questions/50700800/ionic-sqlite-not-running-on-chrome [2023] #001
- SQLite Browser Issue https://ionicframework.com/docs/native/sqlite/ [2023] #002
- Ionic Storage https://forum.ionicframework.com/t/access-sqlite-on-browser/194349 [2023] #003
