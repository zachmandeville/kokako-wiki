<!--Title: Spread -->

A function brought in es6, that lets you insert entire arrays into another array (or entire objects into another object).  It's represented with `...`.

Here is a quick example to get a general idea.

Let's make a band:

`var trio = ['guitar','drum','bass']`

They  need a keyboarder and vocalist:
`var duo = ['synth','vocals']`

We could make a new band, by making a new array that includes each individual item:

`var band = ['guitar','drum','bass','synth','vocal']`

But we already made two variables, that'ssome wasted typing, and we wanna show that it's these two variables combined.

We can use SPREAD!

`var band = [...trio,...duo]`

This is making a new array called band that takes the entire trio array and the entire duo array.  It does the same as what's on line 16, but faster and with better context.

