<!-- TITLE: Pass By Reference -->
<!-- SUBTITLE: The Various Names of Things -->

# Background

Variables are pointers, they are references.

When you declare a variable, the meaning of it will be stored in the computer's memory. 
For example:
```
var person = {name: 'Harrison'}
var anotherPerson = person
```

With the first variable, we've created an object and that object is stored in the computer's memory
in some sorta hash.  The second variable, then, will point to that same stored object.  The first
variable is now a reference to a thing.

It feels like names pointing to a place.  THere can be different names for that thing, but they are
indicating the same place.  And a change to that place will change each of those names too.  There
are multiple names for Mount Victoria.  It is also Tangi Te Keoi

## The case for Primitives 

When a var is pointing to a primitive, and you then assign another var to that first variable, it
doesn't then point to the same primite.  Instead, it creates a duplicate immediately of that thing
and is pointing to that.  

Primitives would be (mostly) numbers, booleans, and strings.  And so if you are creating a complex
object (object or array) it exists as a single thing within the computer that can have multiple
things pointing to it.  But primitives are like abstract values--one variable points to that value.
if another variable points to that concept too, it's not the same object iwthin the computer.  it's
the representative same value.

