# Nodemon

Nodemon is used for restarting the node application and rewritting updated to the application build when code changes have beeb detected. This automatically updated running applications when code updated have occured. This is a Nodemon Cheat Sheet.

## Commands 

### Watch And Execute

Nodemon commands have several parameters that can be included to perform specific tasks. 

`watch` paramater makes nodemon watch a given directory for changes and updates.
`exec` parameter is used to execute other programs than non-node scripts.
`ext` paramater is used to watch for specific file types. An askrisk(`*`) can be used as an all-wildcard.

Example Execution(!ext): `\"cordova prepare\"`.

Example dir(!dir): `www` or `scr`.

Example File Types(!filetype): `html,css,js,ts,php`.

```
nodemon --watch !dir --exec !ext --ext !filetype 
```
