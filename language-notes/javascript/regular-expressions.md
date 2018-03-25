<!-- TITLE: Regular Expressions -->
<!-- SUBTITLE: Parsing Strings using Esoterica! -->

# The Gibberish with Powers
So I don't fully get regular expressions at all.  they are ways to indicate types of characters  within a string,
and then let's your replace or remove them (to remove you replace them with nothing, or '').  These
are full on coded gibberish, so it's just code within code.  but they can be super useful, for example...

# Example Use

`string = string.replace(/[^a-zA-Z0-9]/g, '')`

the RegEx here is `/[^a-zA-Z0-9]/` .  The two slashes enclose the regular expression, sorta how `''`
encloses a string.

The bracket implies a character set, or "Find a match anywhere within this set".

The `^` at the beginning of the line means the _negation_ of the character set.  So "find anything
that _isn't_ any part of this character set"

`a-z` is all lowercase letters from a to z.  `A-Z` is the same, and `0-9` does it with numbers.  [0-9] is
equal to [0123456789]

the `g` means "global" and so searches the entire string for matches.  Without, it would only
replace the first instance in the string (reading left to right).  

Then the two quotes surround the character you'd like to replace all these found characters with.   Since the
character is nothing (the ' is enclosing the character and so '' is enclosing nothing), this is the
same as removing the characters.

And so all in all, take this code:
```js

var string = "Awe%^&*@#$some123"
string = string.replace(/[^a-zA-Z0-9]/g, '')
return string;

```

This is saying: In the string given, find all instances of characters that aren't any lower case
ltters, uppercase letters or numbers.  When found, remove them.  Do this globally, and so find and
remove ALL characters.

When run it will return the string "Awesome123"
