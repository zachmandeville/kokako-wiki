<!-- TITLE: Anonymous Vs Named Functions -->
<!-- SUBTITLE: A quick summary of Anonymous Vs Named Functions -->

# Anonymous vs Named Functions

Anonymous and named functions work in almost the exact same way. Once we recognise what they look like, we can utilise them both!

## Named functions: Examples

> function filter(arr, fn){
    let newArr = []
    for (var i = 0; i < arr.length; i++) {
        if ( fn(arr[i])=== true ) {
        newArr.push(arr[i])
        }
    } 
    return newArr
}


The above function is *named* **filter**. It takes the parameters (arr) and (fn) which iterate into a new Array.

Examples

## Anonymous Functions: What do they look like? 

> server.get('/', function (req, res) {
  res.redirect('/cats') // what is this doing?
})

This server.get function is technically anonymous. Why? If you thought it looked like a "server.get function," I can imagine why! What you've deduced is the type of function it is, but not technically it's name. If a function is named, it will specifically be named (and therefore, later called) between the end of the word **function** and before the **"()"**  round braces that initiate the function.

## Calling Anonymous Functions

??



