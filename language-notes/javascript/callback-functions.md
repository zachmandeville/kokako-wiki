<!-- Title: Callback Functions -->
<!-- Subtitle: Their meaning, their use, their secrets? -->

# Meaning
Callback functions let you ask a function to do a thing, and keep working through your code as it works before it comes back with the result.
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


