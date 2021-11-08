# Cordova

Cordova Cheat Sheet.

## Commands 

### Adding Build Platform  

Having Cordova build our application, setting a platform ffor it to build from will generate the best intended view for the application, this can range from web browser views to native application views.

Example Parameters(!param): `browser`, `android`, `ios`.

```
cordova plaform add !param
```

### Cordova Prepare

Cordova prepare command will install all related plugins to the platform its preparing(e.g. `android`, `browser` or `ios`). When running the application the plugins will install automatically however this command will prepare your application so this isnt done when running for the first time.

Example Parameters(!param): `browser`, `android`, `ios`.

```
cordova prepare !param
```

## Cordova Build 

The cordova build command will build the view within a certain directory or root if no directory is specified. Using the prepared platform target to build from.

Example Parameters(!param): `browser`, `android`, `ios`.

Example dir(!dir): `root/release` == `--release`.

```
cordova build !param --!dir
```
