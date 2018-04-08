<!-- TITLE: Stretch Goal Retrospective -->
<!-- SUBTITLE: How we developed our stretch goal -->

# Introduction
We reached our MVP fairly early, tested and deployed the app by around 2, then had two hours to figure out stretch goals.  One of the goals was to have an owner dashboard,. that showed who was walking your dog.  To do this, we realized we'd need to change our walk request page, create an owner page, and create a table of walk requests.  Zach had a fairly certain path in his head for one way to imnplement this and asked if he could zoom kinda quick through it.  We were able to reach the stretch goal, but the exact way it happened was a bit unclear.  This page is meant to outline the thinking around the implementation and an explanation of the code that ended up working.

# Step One: Work out the Routes.

Our Stretch Goal could be described as so:
- A walker can click on a dog and request to walk them.
- This request is sent to the owner.
- The owner can looka at all requests and choose which one to accept. **

There's three steps to this story, which we can then map nicely to routes.  That was the first thing I did, then.
- A walker can click on a dog and request to walk  => `GET /dog/:id/request` should return a page with a request form.
- The request is sent to the owner => `POST /dogs/%id` should post the form up above.
- The owner can look at all requests, and choose => `GET /owner/%id` should list the contents of each of the received post requests.

# Step Two: Create the Request Form
We know we want to have a request form, and it should come up when you click 'request a coffee' on the dogs page.  And so we can go ahead and make a function that does this for us, _and then_ make the form.

In our `routes.js`page we added the following function:
```js
router.get('/dogs/:id/request', function (req, res){
    res.render('request', {id: req.params.id})
})
```

line 