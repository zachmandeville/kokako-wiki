<!-- TITLE: Meta Tags -->
<!-- SUBTITLE: What they are and how to use them -->

# Background
At the top of HTML pages, within the `<head>` you'll see a bunch of `<meta>`  tags, each with different attributes for their use.  This page describes the ones we've encountered, what they're for, and how to use them!

# The Meta Tags

## meta name: author
This would be the author of the webpage.  Not necessary, but maybe helpful if you want people to know _you_ made this thing.  
```
<meta name="author" content="The Webmaster">
```

## meta name:description
A short description of your homepage.  This is picked first, if available, for the description in search engine results.  without this, the search engine will just print whatever first words you got on the site.  So set this if you want to have a nice summary in the search result (it's also useful for SEO but I don't really care about that?)
```
<meta name="description" content="This is my webpage and it'll be real good check it out!">
```

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
```
        <meta property="og:type" content="website" />
```
**og:type** refers to the actual thing you're sharing.  You can have metadata for images, songs, and videos too (e.g., when you're sharing a youtube link or a bandcamp song).  Each would ahve their own og:type so FB knows how to handle them (e.g.: hide them from anyone's feed so people are trained to upload to FB instead of any other site).      So here yr just saying that yr website is a website.
```
        <meta property="og:description" content="My website has something for everyone.  Really, you should check it out!" />
```
**og:description** refers to the block of text right after the title.  So put something specific and good here most likely, so people know _what_ they're clicking on.
```
        <meta property="og:image" content="http://cdn.weruletheinternet.com//wp-content/uploads/images/2012/february/dog_shopping_cart.jpg" />
```
**og:image** refers to the thumbnail image shown right above the block of text.  It will likely come from your site, but you will want to give the domain path (eg: https://mywebsite.com/path/to/picture.jpg instead of just /path/to/picture.jpg)
```
        <meta property="og:url" content="https://mywebsite.com/" />
```
**og:url** determines the link they show in light gray at the bottom of their block, so folks can know where exactly they gonna go when they click on this facebook share.

## meta name=twitter

Like facebook, twitter has it's own proprietary standard.  It's basically the same, but it means you have to put it in again special for them!

```
  <meta name="twitter:card" content="summary_large_image" />
```

Twitter has different 'card types' for their links (similar to the og:type).  by choosing summary_large_image you'll get the title, description, and representative image.  
You can find out about all the types here: [twitter developer docs](https://developer.twitter.com/en/docs/tweets/optimize-with-cards/overview/abouts-cards)

```
<meta name="twitter:title" content="My Good Website" />
```

This is equivalent to og:title

```
        <meta name="twitter:description" content="My Website has something for Everyone!" />
```

This is equivalent to og:description

```
<meta name="twitter:image" content="http://cdn.thefunnybeaver.com/wp-content/uploads/2015/04/cute-puppy-sleeping-in-shopping-cart.jpg" />
```

This is equivalent to og:image





