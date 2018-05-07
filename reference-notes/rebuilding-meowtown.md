<!--Title: Rebuilding Meowtown -->
<!--Subtitle: Rebuilding a classic as a React and Redux App -->

# Intention

- Revisit Past Concepts
- Better Understand React and Redux by building up an app from scratch.
- Understand how to write API's to then build databases around them.
- How to test an app through and through.
- Have a bunch of good pictures of Charlie to give Angelica.
- Deploy using netlify and...heroku maybe?  That Db would have to live somewhere.

# The App

It'll be a variation of meowtown called 'CHARLIETOWN' that is only concerned with a single meower: Charlie. With this app, you can see pictures of charlie, click on them to get more details, add your own, and delete them.  There should be an admin section for the creation of new pictures, so that the main app is just sharable.  BUT! we can worry about that later.

# The Process

## Clone down Meowtown, and run it, to get a feel for it again.
## Make new Charlietown Repo and initialize with basic README
You can view the repo here: https://github.com/zachmandeville/charlietown
## Write up small set of User Stories for this Charlietown Repo, so there's a clear plan for what I wanna build.
The userstories are also written on the README.  I am essentially working in public, and when they all done I can remove them from the README.  By keeping that readme honest and transparent, I am hopefully letting others  know the state of the app and code.
## Get a working Charlietown client that just displays 'hello charlie', but uses an element of react and redux so they working.
- You can use this boilerplate: [Building up a React and Redux Boilerplate](/reference-notes/react-and-redux-boilerplate)
## Write up API in README that can theoretically fulfill the user stories.
The API is sorta like a technical user story, displaying code you shoudl receive based on route you put in and through this you can tell a story about what should be possible with your database and your app.  
## Create an initial seeded knex database to hold the good pictures and details.
First, install the necessary dependencies;

```
npm i knex --save-dev
```

## connect the database to the react app through the api.
## Prosper


