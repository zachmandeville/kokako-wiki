# Good things to Know

* When using rendering, express knows to look in your views folder.  so you don't have to give a path.  res.render('home') will look, automatically, for the home.hbs file in your views folder.

## The Each convention
You can run through an array with {{#each nameOfArray}}thing you wanna do{{/each}}

## Each Partials
With express-js, our partials are streamlined so we don't have to use the conventions shown on the handlebar.js homepage.  

Now, each partial can be stored in the partials folder (within Views).  Each partial should be it's own file, and the name of that file will be how you reference it in yr .hbs page.

In other words, this partial:
```html
<!--cool-things.hbs-->
<h1>These are  cool Things</h1>
<ul>
<li>ice cream</li>
<li>boom boxes</li>
<li>surfboards</li>
</ul>
```
Can be referenced in your view with:
```html
{{> cool-things}}
```

and that entire HTML block will display in place of that {{}} snippet.

## reg.param:ids
We talked about this at lecture, but I coudln't quite see the code itself and so not sure what to put here but i'ma research more later!
