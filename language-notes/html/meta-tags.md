<!-- TITLE: Meta Tags -->
<!-- SUBTITLE: What they are and how to use them -->

# Background
At the top of HTML pages, within the `<head>` you'll see a bunch of `<meta>`  tags, each with different attributes for their use.  This page describes the ones we've encountered, what they're for, and how to use them!

# The Meta Tags
## meta Charset
This determines how the characters in your html are encoded.  It's useful for when you have special characters (not letters or numbers) in your html posts that you want to be displayed properly.

If all your quotations are showing up as `â€œ` and all your apostrophes as `â€™`, it's likely cos you don't have this meta tag added to yr html.  
The standard encoding for charset is utf-8, and so you'd want to place this meta tag in your `<head>` code would look like:


```html
<meta charset="UTF-8">
```

## meta name=viewport
This tag tells the browser to use the width of the device currently accessing the webpage to determine the sizing of that page.  It's used for responsive websites.  Or, more specifically, this tag is used to make responsive sites work:
```html
        <meta name="viewport" content="width=device-width, initial-scale=1" />
```
This says, essentially, "Wherever there is width defined in the html and CSS, base that width on the width of the device."  
If you are checking your page on the phone and everything looks super small and zoomed out, it's likely cos you're missing this tag.

## meta property:og
There's a number of tags that fall withing this 'property: og'.   All together, they determine how your site is displiayed on facebook when shared as a link.  The og stands for Open Graph, which is a proprietary metadata format designed by facebook for facebook. 

When a site is shared on FB, it'll be shown as a block object with a title, description, image, and so on.  og: determines all of these.
```
<meta property="og:title" content="My Beautiful Website" />
```
**og:title** Refers to the header at the block, naming the link yr sharing.




