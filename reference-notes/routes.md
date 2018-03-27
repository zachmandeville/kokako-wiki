<!-- Title: Routes -->
<!-- Directing The Traffic -->

# Background

We've been putting all functions into our server.js file, when doing the server-side rendering. As our pages will get more complex, that single file could get messy--especially when wwe are trying to collaborate as a team.

# Routes Folder
So now we are making a routes folder, that can take requests and direct them to the appropriate view.

Within the folder, we can put in the different routes (like one for /cats and one for /dogs).  

# Necessary Headings in a routes/route.js file

```js
const express = require('express')
const router = express.Router()
```

This calls in the express module and the function in that module called Router, which takes in the server redirects and sends them to the appropriate rendering.

# The Hotel Metaphor

The server is a super fancy hotel with all the amenities you need.  It has a restaurant, a spa, rooms for every person, a meeting room, and so on. The initial server.js is the front desk, where you are given directions to the different spaces.  But within each space, there'll be someone else at the front to help you.  So you'd have hotel.com where you ask about getting to the restaurant.  The server directs you to hotel.com/restaurant where the restaurant.js file asks you where you'd like to sit and what you'd like to have.  You could have a hotel where the front desk does absolutely everything, but they are going to burn out quick.

# Things to Remember.

A route function looks like our server.get function but says `router.get` instead.  BUT!  the root directory is going to be wherever you've routed to.  And so, if you went to /cats, then the home _at_ /cats would be referred to as '/'.  

_place an example here!_




