<!--Title: React Routing -->
<!--Subtitle: All about routing and react.  I don't know what else to say! -->

# Summary
These are notes about how to direct people to diff. views based on how they've interacted with our page.  Doing the express router stuff, but with react now basically.

#Internal Linking
This is how React does its magic, and it's one of the older tools of the HTML trade: internal links...or anchor tags.

Internal links let you mark and link to sections of a website.  i.e. coolguy.website/coolshit#skateboards will take you to the skateboards section of my coolshit page.  It's not having to load a new page each time, but instead display a new section of that page.

# Destructuring

This is a thang we learned during our react router exercise.  It's a quick way to assign variables for each property in an object.  for example, let's say we have this object:

```js
myObject = {
  cats: ['cat1', 'cat2'],
  dogs: ['dogA', 'dogB'],
  otherStuff: {
    coolStuff= ['skateboard','weed'],
    dumbStuff = ['getting sick', 'traffic jams']
    }
}
```

If I wanted all my cats, I could write `myObject.cats`.  If  I didn't want to have to write that the whole time, I could insted declare a variable like: `var cats = myObject.cats`.

But, if I didn't want to have to declare a variable on a new line each time, I can DESTRUCTURE.  It looks like this:

`{ cats, dogs, otherStuff } = myObject`

This makes a variable for each property in myObject named after that property.

# Router and Route

Both are components of React.  It allows you to set up diff. routes, that are actually just sections of the same webpage.

```
<Router>
  <div>
    <h1>React!</h1>
    <Router path='/' component={Home} />
    <Router path='/about' component={About} />
  </div>
</Router>
```

Now when we load the home page, we show the home component.  Or rather it'd show as `www.coolguy.website/#`  meaning that it's going to the anchor of home in that single page of coolguy.website.

When I go to about, it renders `coolguy.website/#/about`.  This will display both the home page component _and_ the about component.  this is because React wants to render everything possible.

To only show the about page, you'd change Home up above to:
`<Router exact path='/' component={Home} />`
Which says "only render the home component when you go to the _exact_ route of `coolguy.website`

# <Link>
Another React component.  This allows you to set up quick links to other sections.  so in the home area, we could write 
```
<h1>here is my home page</h1>
<Link to='/contact'>Contact Me!</Link>
```

This would create an <a> tag in the browser, that brings you to the contact section.

# Browserrouter

server.get('/*', (req, res) => {
  res.sendFile(path.join('__dirname'), '../public.index.html'))
}

Mix that with, in the App component `import Browserrouter from react`

quick note: By default, React will render all possibles. So if you 
