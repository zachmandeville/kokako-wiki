<!-- TITLE: For Loops -->
<!-- SUBTITLE: The Old Standard -->

# Our reliable friend For Loop
For loops let us loop through all the items in an array.  They've been replaced, in many cases, by the higher order functions map, filter, find, and reduce...but they are still useful in their own way.


With for loops you put in all the constraints _within_ paragraphs at the beginning of the loop.  You
place a starting condition, a condition to continue, and an ending condition. 

```js
for (var i = 0; i < 5; i++) {
  ourArray.push(i);
}
```

This would mean we'd push the number (i) into the array for each loop.  It will start at 0 and continue utnil i is no longer less than 5....in other words youd create an array of [0,1,2,3,4]

Arrays and for loops and objects have _so_ much power.  I know I am just scratching the edge of it.

In the for loop, having it say, explicitly 'var i' or 'var whateverYouWant' is crucial.  You cannot
forget the var....sometimes it will work and sometimes it doesn't and you won't know why it's not
working....so just be diligent with that sweet var!
