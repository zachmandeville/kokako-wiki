<!-- Title: Async Functions -->
<!-- Subtitle: further notes about async functions -->


# Summary
Asynchronous functions are a common function type in javascript programming (and especially node programming).  They allow you to run a function without interrupting the rest of the code running.  It runs asyncrhonously from the rest of the code.  In this way, you can have multiple processes running at once (e.g.: displaying an interface while the background processes are loading).

# Midnight Espresso Analogy

When you go to Midnight Espresso, you order a coffee, and then just have to wait until the coffee is finished.  The line is held as the cashier makes coffee and you stand by the counter.   Then the coffee is given to you and you can sit down.  This is **synchronous**.

Other coffee shops will give you a number right after you order.  Then you can sit down, do your thing, not think about the coffee _until_ it's finished.  At that moment, the cashier calls your number, your return and grab your coffee.  This is **asynchronous**.  The cashier offered you a **callback** to let you know their coffee-making function was done--but did this without interrupting yr own flow.


# File List vs. User Selection

When accessing files in a list, it comes as an array.  If you were to turn this then into an object, the order of each line isn't set.  The object could pull 4,1,2,3,0 from the array instead of 0,1,2,3,4.

The array's order will stay though.  So in the case where you want to assign a number to each file, use the array and i as the index of that array (using those sweet for loops).

# fs.readline

Here's some basic code with some notes!

```js
fs.readline(){
std.in \\ A stream of characters from the user to the console.
std.out \\stream of characters to be printed to the console.

rl.question('What you want to ask the user', function(input){
  rl.close \\This stops the stream, just a part of the readline function for safety (I believe!)
  what happens here is whatever you want to do once the user selected something.
  })
  }
```
  
# Refactoring

Let's take this bit of ascii code as an example:

```
const fs = require('fs')

function go(){
   var rl = readline.createInterface({
    input: process.stdin,
    output: process.stdout
   })
  console.log('Welcome! We are so glad you are here!')
  fs.readdir('./data','utf-8', function (err,files) {
    console.log('here they are!')
    for(let i = 0; i < files.length; i++) {
      console.log((i+1) + ': ' + files[i])
    }
    rl.question('Which File should I load?", function (input) {
      rl.close()
      console.log('you chose ' + input)
      fs.readFile('./data/' + files[input-1], 'utf-8', function(err, data){
        if(err){
	  console.log(err)
	}
	else{
	  console.log(data)
	}
  })
}

```

Essentially, you are needing to call a function inside another function inside another function, etc.  The more you wanna do with the result of that first data call, the more you are nesting functions and the more horizontal and confusing your code becomes.

We can break apart some of these nests into their own functions, so that the go() function is more readable.  The trick is to give these new functions arguments to be given, so they have the proper scope.

```js
function displayFile(file) {
  fs.readFile('./data/' + file, 'utf-8', function(err, data){
    if(err){
      console.log(err)
    }
    else{
      console.log(data)
    }
```

Now that reading of the input can be handled by it's own function.  This means you can write:
```js

  rl.question('Which File should I load?", function (input) {
    rl.close()
    console.log('you chose ' + input)
    fs.readFile('./data/' + files[input-1], 'utf-8', function(err, data){
      if(err){
	console.log(err)
      }
      else{
	console.log(data)
      }
```

as:

```js
  rl.question('Which File should I load?", function (input) {
    rl.close()
    console.log('you chose ' + input)
    displayFile(files[input-1])
```

MUUUCH more readable and reusable!!  The trick here is that the function you wrote has a parameter(the `file`).  And so now you can pass a parameter to it from within the larger function (that's the `displayFile(files[input-1])` part).  

So you can refactor by isolating and writing functions, as long as they have the ability to accept variables that were defined before.  If you don't give them that option, they ain't going to work!


# Good to Knows
* There isn't any visible difference between a synchronous function and an asynchronous function.  It's all about the implementation in the function itself.  This is why it's good to label your synchronous or asynchronous functions, so the person using (or reviewing) your code knows how it's expected to work.

* It's common, when writing async functions, to do "error-first"  which means, essentiall "if there's an error, return the error message. Otherwise, return the results.")



# Examples

**A straight ahead function would be like this:**
```
function doWork(myFunc){
  myFunct()
  }
  
console.log('about to do work')
doWork(function(){
  console.log('doing the work')
  })
console.log('all done)
```
This will output to:
```
about to do work
doing the work
all done
```

The purpose of that do work function is to do a function, which is defined in the argument you pass it.

**A callback function would be like so:**

```
function doWorkAsync(myFunc){
  waitThreeSeconds()
  myFunct()
  }
  
console.log('about to do work')
doWork(function(){
  console.log('doing the work')
  })
console.log('all done)
```
This will output to:
```
about to do work
all done
doing the work
```
The aSync function has a command to wait a few seconds..the code itself doesn't wait..it keeps pushing forward and so when the function does run it returns its value.  This is why the lines seem to be out of order.

# Uses

When you are working with a network, or accessing a database, where the act of sending a message to the databse to return a thing may take longer than the other functions.  In this way you can have a program running, that returns database results, but doesn't have to wait for the results to keep running the rest of the program.


# Meaning
Callback functions let you ask a function to do a thing, and keep working through your code as it works before it comes back with the result.
