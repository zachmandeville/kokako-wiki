<!-- Title: Variables as Functions -->
<!-- Subtitle: What happens when the variable is a function! -->

# Background

The classic way to write a function is so:

```js
function affirmation () {
  console.log('Hell yeah you're great!)
  }
```

But it can also be written as so:

```js
var hellyeah = function () {
  console.log('Hell yeah you're great!')
  }
```

Both can be called with `hellyeah()`, but there's some important differences!

# Differences

A key difference is that you have to declare the variable before you call the function.  This is not necessary if you define it as a function instead.  

In other words, this will run:

```js
affirmation()

function affirmation () {
  console.log('Hell yeah you're great!)
  }
```
But this will not:
```js
affirmation()

var affirmation = function () {
  console.log('Hell yeah you're great!)
  }
```
This is due to how the javascript interpreter parses the file at the beginning.  It looks for all functions first, then runs the program from top to bottom.  In the latter example, the function is basically hidden inside the variable and so the parser doesn't see it before executing the script.  You'd get an error, then, that `affirmation is not a function` since it tried to execute before the variable was defined.

# Module.exports

It is for this reason that it's great to put [module.exports](module-exports) at the bottom of the file.  You may need to export a function that was defined as a variable.  If you place module.exports at the beginning, it's going to try to export something that isn't defined yet (like the example above).  If it's placed at the bottom, you know that all the functions have been defined whether as variables or not before yr trying to export them.


