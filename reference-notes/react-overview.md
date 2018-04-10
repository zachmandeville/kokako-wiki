<!--Title: React Overview -->
<!--Subtitle: Everything you need to know to have the best reaction to React! -->

# Background
A tool for client-side rendering.

# Concepts

## Client-Side Rendering
Instead of having the server render and serve a webpage to the client(the browser), you instead ask the client to render the page on the browser as they access it.

##bundle.js
The output of an application called webpack that has been _transpiled_ into javascript.

##Sass
A language for styling that gets transpiled into CSS in the browser.

##JSX
javascript markup language.  Another template language, like handlebars, but different!  Important thang is that it takes one curly brace, and within that you can put in entire functions.  handlebars on acid.

##Webpack
Webpack is an open-source JavaScript module bundler. Webpack takes modules with dependencies and generates static assets representing those modules.  We will be using it going forward, but may not have to understand _exactly_ what it's doing.

## difference to Handlebars.
In handlebars, we make up views that we feed data into.  So we are having to still make up static pages, that have variables placed in for us to fill out with whatever data we are feeding in.  With React, you can instead write up the templates as functions, to have them be small and specific and using the power of JS.

# Basic React Setup for Homepage

```js
var React = require('react')
var ReactDOM = require('react-dom')

function myTemplate(data) {
  return <h1>Hi there {data.name} </h1>
  }

var data = {name: 'harrison' }
var view = myTemplate(data)

var placeToMount = document.getElementById('root')

ReactDOM.render(view, placeToMount)
```

This will render a page that says 'Hi there Harrison!' within the div with an id of 'root'.

## Having multi-line HTML

In the above code, I was only rendering a single line of html: `<h1>Hi there {data.name} </h1>`.  If I were to add a second line beneath, like `<p>how you doing</p>`, then this second line will not be rendered as javascript tried to be helpful and added a semicolon at the end of the first line.  To counteract this, we can wrap the two lines in a parenthesis to tell the function we ain't done:
```js
function myTemplate(data) {
  return (
    <div>
    <h1>Hi there {data.name} </h1>
    <p>how you doing</p>
    </div>
  )
}
```
We also added a `div` tag here, too, as a particularity of React.  You cannot pass on two or more sibling functions.  React only wants a single top-level function.  So we add the div, and pass on the div, and within it is our thangs we want.

# Component
The partial views, essentially.  We are moving away from the language of templating, and into components.  so this is straight up a new concept.

A couple rules about them:
- They always start with a capital letter.  so `myTemplate` becomes `MyComponent`
- You can add components within each other with `<MyOtherComponent />`

# Keys and the Shadow DOM
React keeps its own copy of what it tinks the DOM should look like in memory - the shadow DOM.. it then looks at what the difference between the DOM/Shadow DOM is and only changes the parts that are different...
To do this it needs keys. You may find an error in your browser without them.

```function App (props) {
	 return (
	 <div>
		 {posts.map(post) => {
			 return (<Post key={post.title} title={post.title}/>)}}</h1>
	 </div>
 )
}
```

# Import, Export

These are new features of es6 based off the require module in npm.





