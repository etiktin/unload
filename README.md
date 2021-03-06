# javascript: unload

Run a piece of code whenever the javascript-process stops/exits/quits. On **browsers, nodejs, election, react-native, .net-core**. It also ensures that the exit-function is called only **once**.

You should use this module when your write a npm-library where you dont know in which environments the users will run it.

# What does `unload` handle?

When nodejs:
```js
process.on('beforeExit')
process.on('exit')
process.on('SIGINT')
process.on('uncaughtException')
```

When browser:
```js
window.addEventListener('beforeunload')
```

When electron:
```js
app.on('window-all-closed')
```



# Usage

Installation:

`npm install unload --save`

Add a function which runs when the process exits:

```javascript
var unload = require('unload');
unload.add(function(){
  console.log("Ouch, I'm dying.");
});
```

Add and remove the function (It will no longer run when the process exits):

```javascript
var unload = require('unload');
var stopListen = unload.add(function(){
  console.log("Ouch, I'm dying.");
});

stopListen(); // removes the event-listeners
```

Run all previously added functions:

```javascript
var unload = require('unload');
unload.add(function(){
  console.log("Ouch, I'm dying.");
});

unload.runAll();
```

Remove all added functions (They will no longer run when the process exits):
```javascript
var unload = require('unload');
unload.add(function(){
  console.log("Ouch, I'm dying.");
});

unload.removeAll();
```
