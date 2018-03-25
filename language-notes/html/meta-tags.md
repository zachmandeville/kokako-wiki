<!-- TITLE: Meta Tags -->
<!-- SUBTITLE: What they are and how to use them -->

# Background
At the top of HTML pages, within the `<head>` you'll see a bunch of `<meta>` tags, each with different attributes for their use.  This page describes the ones we've encounters, what they're for, and how to use them!

# The Tags
## Meta Charset
This determines how the characters in your html are encoded.  It's useful for when you have special characters (not letters or numbers) in your html posts that you want to be displayed properly.

If all your quotations are showing up as `â€œ` and all your apostrophes as `â€™`, it's likely cos you don't have this meta tag added to yr html.  
The standard encoding for charset is utf-8, and so you'd want to place this meta tag in your `<head>` code would look like:


```html
<meta charset="UTF-8">
```

