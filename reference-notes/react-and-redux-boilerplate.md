<!--Title: Building a React and Redux Boilerplate -->
<!--Subtitle: A personal journey towards a personal boilerplate -->

# Summary

This is a series of steps taken to make a boilerplate, and why each dependency and structure was chosen.  The goal is to not just have a file to be used, but a reason behind the file.

# Wants

- Simple, and not too heavy.
- React and Redux being used.
- Browserify instead of Webpacks if possible.

# Strategy

Build complexity when necessary, build extra files only when necessary.  Don't overcomplicate from the start.
use hello world before you build a choir that each speaks one letter of hello world.

But also know that react is a framework _for_ complex apps, and so has necessary complexity built in so you can expand.  Much of the confusion you have around it is because you are starting simple within a framework that is expecting a city of things.


# Steps

## 1.) create a git repo and clone it to yoru computer.  Then cd into that repo.
## 2.) initialize this repo as an npm repo
In other words, say 'in this directory node shall live.'  So, let's invite node in:
`npm init -y`

This invites node in, sets up a package.json for it, and fills it with some default properties.  the -y means 'say yes to anything the initializer asks me'.  Without it, you can fill out a description of this 'module', who you are, what license it under, etc.
## 3.) Install react and redux dependencies.
React will handle the front end and displiaying whatever data we give it.  Redux will handle the statemanagement (the backend of sorts) and will be passing the data to react for it to display.

We can install all them dependencies at once with:
`npm i react react-dom react-redux redux --save-dev`  the i means 'install', we thenn list every npm module we wanna install, and we save it to our package.json under the devdependencies property.
## 4.) install browserify as a bundler
browserify bundles up all our various modules and folders and dependencies into a single bundle.js file, so that everything can be run client side.  It has other dependencies to help it out too.  So the full install of this portion is:
`npm i browserify watchify tinyify babelify --save-dev`

installing browserify, watchify (to run a live-reload 'watch' mode of our client), tinyify('to minify all the code we are running, so that bundle.js file is smaller and faster), babelify(to use 'babel' with browserify.  babel translates es6 code down to es3, so your site can be viewable on older browsers).
## 5.) Install babel dependencies.
These dependencies just help babel work, and tells it _what_ you want babelified and to whaat other thing.
`npm i babel-core babel-preset-es2015`
## 6.) Install budo, for 'deploying' your site to local host.
To have all the code run on the client, we need to first bundle it up.  But what if we wanna see how it'll look before it's bundled?  For that, we need to make a pretend server of sorts, that can serve up all our files to the localhost and make the app run as if everything were bundled.  This helps us whend eveloping, so we can see the effets of our changes without having to run 'npm run build' everytime we make a change.  

The module that helps us with this is budo.  So we install that now too:
`npm i budo --save-dev`

## 7.) Write some Scripts!
These scripts help us start, experiment upon, and ultimately build our site.  They are written in the scripts section of package.json

`"build": "browserify index.js -t babelify -p tinyify > bundle.js"`
`"watch": "watchify index.js -t babelify -p tinyify -o bundle.js",`
`"dev": "budo index.js:bundle.js --live --open -- -t babelify"`

for build it's saying 'browserify my index.js file using the transforming powers of babelify and the prettying powers of tynify and then take that fully browserified thing and write it into a file called bundle.js'

for watch it's doing the same, but now for watching...so it's not bundling up anything, it's pretending there _is_ a file called bundle.js that we'd be using.

dev is having budo do that same transformatioin, then offering live reloading and oepning the page automatically for us, and remembering to babelify it at the end.

## 8.) Make .gitignore and .datignore

```
node_modules
bundle.js
*.swp
.DS_Store
```

We don't need the repo seeing any of these files.

## 9.) Make .babelrc

V IMPORTANT

## 10.) Set Basic Folder Structure

The essential files you gonna need are:
* index.js
* index.html
* component/app of some sort

What we do, then, is start up a simple index.html page that has a div that is waiting for javascript to load within it, like a square of soil waiting for a seed.

In our index.js file, we say 'if you find a spot of soil, plant our component called app inside it'.  Then in our app file we say, "I display this html when called upon.  I am ready to be called upon, if there is a place to have me.'

When you run the build script, it'll bundle up all your javascript into a single bundle.js file that is called upon in your index.html.  And so your browser is only opening the index.html, but everything is sprouting from within that one div.

## 11.) Add Redux
### 11a.) Add reducers folder and actions folder
Reducer is gonna be our dispatch, that listens for messages from anywhere in the app, and responds by doing the necessary action.  In most cases this is going to be changing state in some way.

Anytime state is changed, the app renders again--so it allows for dynamic displays based on how you displaying that sweet state.
### 11b.) Add state to reducers/index.js
```js
var initialState = {
  fear: ''
}

var fearEater = (state = initialState, action) => {
  switch (action.type) {
    case: 'ADD_FEAR':
      return {fear: action.fear}
    default:
      return state
  }
}

export default fearEater
```

this is an example app.  It creates an initial state, which is going to be an object with a bunch of keys.  You can have as little or as many as you want as actions handled by the dispatch may add new keys to the state.

Below that you have different 'reducers' which listen for events and ask the right action to do it's thing.

### 11c.) Add action to actions folder

These will be the signals for action to occur, they are ojbects that include type and some other value (or more than one value).

### 11d.) Add state to root index.js

We want to be able to pass along the properties of State to every component within our app.  We can do this using the Provider module from react-redux, and wrapping our whole render in the Provider tag.  We also want to initialize a store, so we can pass that into the Provider.

I kinda hate the terms Provider and connect because they dont' make any aesthetic sense to me, so I cannot give a good reason why you are wrapping this tag, other than to remember these two things because it makes the rest of the app just kinda work nice.

```js
//initialize a store, using our fear reducer
var store = createStore(reducer, 
  window.__REDUX_DEVTOOLS_EXTENSION__ && window.__REDUX_DEVTOOLS_EXTENSION__()
)

//render our App component once the entire DOM loads,
//and place that sweet man within whatever has the id
//of 'root
document.addEventListener('DOMContentLoaded', () => {
  render(
    <Provider store={store}>
    <App />
    </Provider>,
  document.getElementById('root')
  )
})
```

##11.f) Make yr components aware of state.

So now each component has to be aware of state.  We can do this by passing along the state as properties 
that the component can render.

We do this by giving them props when they are defined,
then mapping state to those props, so whatever is in state now is in the components property, ready to be called.

##12.) Test!









