<!-- TITLE: Data Coercion -->
<!-- SUBTITLE: When a thing can't truthfully become another thing -->

# Definition
When you give a type that is different from what javascript was expecting.  you give a number when
it's expecting an object, or a string when it's expecting an object.

This comes up with truthiness or falsyness.  Where different types are coerced into truthy or falsy
(in other words (i think) it'd be true enough or false enough).

# Example

`if(name) console.log('hello ' + name)`
this truthiness coms out to mean "say hello name _if_ the name variable is filled out.  If it's null
or empty, then those are falsy and so would not fit that if statement: 
if (name = true) then say hello name.  

