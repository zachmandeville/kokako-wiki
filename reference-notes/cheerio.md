<!-- Title: Cheerio -->
<!-- Testing The HTML Strings themselves. -->

# Purpose

Essentially jquery _for the node generation_.  It returns the text in your http response into a queryable thang.  So you can use this in testing to say "I expect the h2 with the class "title" to say 'Good Ass Website', for example.

# Example

```html
S('h2.title').text()
```
This would mean: 'return the text for the h2 tagged item with the class of title.'



