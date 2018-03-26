<!-- Title: Handlebars -->
<!-- Subtitle: Making web templates look as good as a well-waxed mustache -->

# Background
# Key terms
# Cool Examples

In the template html page, you'd have:
```html
We are open on these days:
<ul>
{{each days as |day|}}
<li>{{day}}</li>
{{/each}}
```
And in yr server.js file, you'd have:
```js
server.get('/', function (req, res) {
  res.render("home", {days: ['Monday', 'Tuesday', Wednesday']}
//Essentially, I don't remember the full code here tbh
}
```

This would take the days object, and run a loop through it to grab each day from the array, and then list them as their own <li> tag.  V. Cool!
