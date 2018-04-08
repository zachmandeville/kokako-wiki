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
## Write the Function
We know we want to have a request form, and it should come up when you click 'request a coffee' on the dogs page.  And so we can go ahead and make a function that does this for us, _and then_ make the form.

In our `routes.js`page we added the following function:
```js
router.get('/dogs/:id/request', function (req, res){
    res.render('request', {id: req.params.id})
})
```

The first line sets up a basic get function based on how Express likes it (start with the url we are getting a request for, then call a function that takes request as the first argument and response as the second argument).

The second line **res**ponds with a rendering of our 'request' view.  Since this view will be using handlebars, and we can pass objects into handlebars that are then values to be displayed or used by that particular page, we decided to pass along the id of the dog as an object.  We didn't fully know what we'd do with this yet, but figured our ultimate 'walker request' table would want to know the id of the dog to be walked, we decided to go ahead and pass that on.

## Write the Form
So we know we wanna render a view called request, so now we just have to write it up in html.  We saved a new filed called `request.hbs` in our `views` folder.  We don't need to know what our table or style or future is going to look like.  We can just code it up in real time and decide as we go.  

We'll need a title so people know where they are and so we add:
`<h1>Request Walking a Dog</h1>`

We also know that we want to ultimately pass a form, so we just add a form 
`<form action='/dogs/{{id}}' method='post`
`</form>`

The action says where to submit this form once the user presses submit, and the method tells the form _how_ to submit it.  In other words "send the contents of the submitted form as the body of our POST request to /dogs/{{id}}".  We don't have a function for that yet, but that's fine, cos the form is saying we should _make_ function to handle it. The ID in that action will be whatever dog page we are currently at, and it's being pulled from that route function we defined above through the magic of handlebars.

So now we just need to fill out the form.  At this point we think about the requests table we are hoping to make.  We already have a table about all our dogs which includes a refernece to who owns which dog.  We also already have a table that lists all our walkers.  A walker can have many dogs they walk, and a dog can have many requests from walkers to walk it.  soooo....we need a many to many table.  This table should include the dog id, and the walker id.  

This is also a 'request' not a confirmation.  That confirmation should be done by the owner.  So there should also be a status of the request, saying whether it's pending, denied or returned.  Any new request should have a pending status (since it'd be odd to submit an already denied or approved request).  

So our dogs_walkers table really only needs these things:
`| dog_id | walker_id | status `|

Our form page already has the dog ID on it, so that doesn't need to be submitted.  The status is not set until later, and so this form doesn't need to handle it either.  We don't have a walker login, though,. and so we _will_ need to have the form submit the walker's id.  

We realized, then, that the form only really needs a single question: "who are you"?  We can join and reference and all that to fill out the other details later.  

And so: our form looks like this:
```html
<label for="walker id">Who Are you?
    <select name='walker_id'>
      <option value="1">Sabrina</option>
            <option value="2">Lt. Surge</option>
      <option value="3">Koga</option>
      <option value="4">Red</option>
      </select>
</label>
<input type='submit' value="Request that Dog!">
```

- The `label` tag handles the line that appears above the form's input area.  
- The `select` tag says the form will be a dropdown, with multiple options to select from.  The name attribute determines what property this option will be submitted as (in other words, if the form submits an object, then this name attribute says the object will look like so `{name: something}`)
- The `option` tags set what will appear in the dropdown.  This is where we can be a bit tricky.  Within the options tag we can set the `value`.  This is what will be passed in to our form object.  BUT!, the _value_ doesn't need to be what we _show in our form_.  That's determined by whatever we enter between that option tag.  So we looked at our walkers table, put their name in as what shows on the form, but set the value to be their walker ID.  This means that Sabrina can  pick her name from the name list, but it gets passed along as `{walker_id: 1}` to our database table.  Fun!

Our view is now done!

## Make a Table
This doesn't need too much explanation.  We made a new migration for our walker_dog table, that had the columns we listed above.  Then we migrated this table up.  Once we had the table, and the form to add stuff to it, we just needed a function that handled how things were added.

# Step Three: Post our form to our dog_walker table
## Write the route function.
We know that we want to add content to a table when a form is posted.  So we can go ahead and make the route that says this.  We don't have to worry how it'll all work yet, the route just essentially describes _what_ will happen, not how.

So we write a route like so:
```js
router.post('/dogs/:id', function (req, res){
    db.submitRequest(req.body, req.params.id)
      .then(function (request) { 
          res.redirect('/dogs')
      })
})
```

- The first line is a basic route function.  
- The second line says we'll call the submitRequest function from our db.js file.  The submitRequest function doesn't exist yet, but it _should_ exist, so we'll write it assuming it does. 
- Similarly, we know that we want to add the dog_id and walker_id.  The walker_id is part of the form we are submitting, so we'll say we are pasing it along with `req.body`.  The dog_ID is a part of the page URL we are posting to, so we can pass that along with `req.params.id`.
- We want submit to add both to our database, so we'll know we're using knex to do so.  Knex works with promises, which return a value you then do something with.  So we know that after our submitRequest function we can do a `.then` function that passes along whatever value is returned.  We don't actually do anything with this returned value.  Instead, we redirect to the /dogs page.  That redirect is kinda arbitrary, but it made sense that after you submit the reques,t the walker would wanna return to the page with all the dogs to request a walk with another dog.

## Write the submitRequest function
We said there'd be one in the db.js file, so we navigate to there and write up a new function called `submitRequest`
We also said we'd be passing along a body and id.  So we add two arguments to our function (plus a third testDb argument for future testing.  At the start, then it'll look like this:

```js
function submitRequest(body, id, testDb) {
}
```

Utlimately, we want to pass along a new line to our dogs_and_walkers table.  Knex lets us do this by passing along an object into our insert function.  These objects should have keys for the different column names in the table. So if Charmander (dog 1) got a request for walking from Red (walker 4), we would want to pass a new object that looked like this:
`{dog_id: 1, walker_id: 4, status: 'pending'}`

1 is equal to the req.params.id which we are passing along as our second argument.  In other words, we can rewrite that above object to be:
`{dog_id: body, walker_id: 4, status: 'pending')`

The body argument in our submitRequest function is a  stand-in for req.body.  `req.body` will pass along an object, that contains whatever value we submitted in our form.  In other words, `body` is equal to `{walker_id: 4}`

We can reference keys iwthin an object using dot notation, so we can reference our walker_id in our req.body using handy dot notation.  That means we can rewrite our insert object to be:
`{dog_id: body, walker_id: body.walker_id, status: 'pending'}`

Now we just need to insert that object into our dogs and walkers database.  So the entire function looks like so:
```js
function submitRequest (body, id, testDb) {
  return db('dogs_and_walkers')
	  .insert({dog_id: id, walker_id: body.walker_id, status: 'pending'})
}
```

We can test if this works by opening up our database in the sqlitebrowser.  If I submit a form on Squirtle's page, saying my name is Sabrina, then there should be a new row with: dog_id: 2, walker_id: 1, status: 'pending'.  AND we should return to the dogs page.  

Testing this, all these things pass.  Now we just need to show these requests on our owner's dashboard.

# Step Four: Get the Owner's Dashboard showing Requests
## Think of what we want to show on our Owner's page.

It'd be awesome for the page to say something like: 
**Hello, Misty!**
**Here are the requests for Squirtle**:
** - Sabrina wants to walk your dog // Pending**
**  - Lt. Surge wants to walk your dog //Pending**

Plus a button to add a new dog.  We can rewrite that above site more abstractly to be:
**Hello {{Name}}!  Here are the Requests for {{dog_name}}.  {{Walker_Name}} wants to walk your dog {{Request_status}}**

## Make our route match our vision
We Already had a route function for the owners page that looked like so.

```js
router.get('/owner/:id', function (req, res) {
  db.getOwner(req.params.id)
	  then(function (owner) {
		  res.render('owner', {owner})
})
```

When we get a request, we run a getOwner function using the id passed along in the url.  This grabs the owner's info from the database and renders a page using that info.  If we ignore the walk requests for right now, we can say that the owner's info should include the owner's name and all the owner's dogs' names.  So we'll look at our `getOwner` function to make sure that's the case!

## Adjust the getOwner function

We have an initial function that looks like so:
```js
function getOwner (id, testDb) {
return db('owners')
  .where('owners.id', id)
  .select().first()
```
This looks into the owner database for whatever owner_id matches the url id we are on and selects that.  since the select function returns an array, we want the first item int hat array, so we add the first function.

The owner's table includes the owner_id, their name, their email, and so omether addresses.  It does _not_ include their dog.  This is because an owner can have many dogs.  For our stretch goal, we are only using a case of one owner having a single dog (cos of time contstraints)...but our table is still structured for the future.  

What this means is, if we want to display info about the dog too, then we'll need to grab info from the dog's table that is relevant.  We can do this with a join function.  The dogs table includes an owner_id, so it is simple enough to join the two tables based on that value.  

Lastly, both the owner table and dog table have a column called ID.  If we join them together and select the entire thing, then one of the id's will override the other.  We don't want that, and so in our select function we explicitly say what values we want to select and what we want to now call them.

Our final getOwner function looks like this.
```js
function getOwner (id, testDb) {
return db('owners') //grab the owners table
  .join('dogs','owners.id', 'dogs.owners_id') //join it to the dogs table based on where the owner's id matches the dog tables owner_id column.
  .where('owners.id', id) //from this big joined table find where the id column matches our id value (which is req.params.id)
  .select('dogs.name as dog_name','owners.name as name','owners.id as id', dogs.id as dog_id')//select all the values in these columns, but //rename them as whatever I set.
	.first()
```

Our owner's dashboard can now include the name of the owner _and_ the name of hte dog.  PLUS we now have the dog_id coming back in with all the other info.  So we can use that to find pending requests.

## Check out our owner route again.

If we look at our owner route function:
```js
router.get('/owner/:id', function (req, res) {
  db.getOwner(req.params.id)
	  then(function (owner) {
		  res.render('owner', {owner})
})
```
We can see that we are passing along the object returned in our getOwner function, and thenr endering ap age based ont hat.  We aren't ready to render the page yet though.  We don't want just the owner's info. we want their pending requests.  

So we simply make up a function that describes this and fit that in before rendering the page.

So we rewrite our route function to look like so
```js
router.get('/owner/:id', function (req, res) {
  db.getOwner(req.params.id)
	  then(function (owner) {
		  db.getWalkRequests(owner)
			  .then(function (requests){
		        res.render('owner', {owner: owner, requests: requests})
})
```

We got ourselves a promise chain, and the cool thing about this is that the ending part of the function will remember everything that's been passed along the way.  In other words we can get our owner, and pass along the owner we got to our walkRequests function, which will return the requests for this owner.  We can then use both the returned owner object and the returned requets object in the page we ultimately render.  

Now, let's write that getWalkRequest function.

## Write getWalkRequests function 

We know we're passing along owner info in that above route, so let's make that explicit.  Our starting function then is:

```js
function getWalkRequests(owner, testDb){
}
```

The first goal is to just show who wants to walk the owner's dog, and the status of this request.  We need this info from our `dogs_and_walkers` table.  So we can expand the function to be:
```js
function getWalkRequests(owner, testDb){
  return db('dogs_and_walkers')
	  .select()
```

This is alright, except it's going to return every walk request, regardless of which dog it's for.  We want to only find the ones related to our owner.  Luckily, the owner object we're passing includes their dog_id (since we joined the owner and dog table in our previous getOwner function).  So we can add a variable that says `dog` equals whatever dog_id is in our owner object, and then filter our database query to only the cases where the dog_id equals our owner's dog. In other words:

```js
function getWalkRequests(owner, testDb){
  var dog = owner.dog_id
  return db('dogs_and_walkers')
	  .where('dog_id',dog)
	  .select()
```

This will return an array of requests taken from our dogs_and_walkers table.  If we remember, the table has three columns: dog_id, walker_id, and status.  Our owner won't know people based on their ID, so this selection is kinda useless.  We need the walkers' names so the owner knows what to call them when they get together for coffee.  This info isn't available in this table, but it _is_ available in our walker table.  So let's join them!!  Then, let's explicitly define what it is from theste two tables that we want to select, by stating them within our select function.  This will make writing up the view much easier.

Our final function will look like this:

```js
function getWalkRequests(owner, testDb){
  var dog = owner.dog_id
  return db('dogs_and_walkers')
	  .join('walkers','walker_id', 'walkers.id')
	  .where('dog_id',dog)
	  .select('walkers.name as walker', 'status as status')
```

This is going to return an array of requests.  In other words, it's going to return a list. So as our final thang, let's format the 'owner' view so it can display everything in that list.

# Step Five: Rewrite our owners view.

This is best explained within the html, so here it is in full below!

```html
<!-- Since we've  passed in two blocks of data (owners and requests), we need to specify which block of data we're referring to in each 
of the handlebars. So in this top header we want the name from the owner data-->
<h1>{{owner.name}}</h1> 
<a href='/owner/2/new' title='add a new dog'><button>Add a dog?</button></a>
<h2>Requests for {{owner.dog_name}}</h2>
<!-- Now for each of the requests from the requests data (because a dog might have more than one request) show the walker and an option to 
change the status.  This will ultimately be a form the owner can submit (to accept the request).  So let's just make it a form now.
In the future, we can also filter this to only show pending.  We won't worry about that for right now though, cos of time. -->
{{#each requests}} 
<form action='/owner/:id', method='post'>
    <p>{{walker}} would like to walk your dog.</p> 
    <select name='status'>
        <option name='pending'  selected>Pending</option>
        <option name='approved'>Approve</option>
        <option name='disapproved'>Reject</option>
    </select>
    <input type='submit' value='confirm'>
</form>
{{/each}}

<a href='/'><button>back</button></a>
```

That is really it!  Or rather, we hit 3:30 at this point and couldn't do the form functions and such. so we have a useful start.

# Final Step: Test it!

We can write tests (and we will!) but for now we should be able to click on Charmander (which is owned by ash, owner_id 1), request to walk them and say our name is Sabrina.  Then, when we go to /owner/1 we should see that Sabrina has requested to walk our dog Charmander, and a dropdown to choose whether we want to leave it in pending, approve it, or disapprove it.

Upong running through this story, all the parts work.  We did it well enough to present!

# Wrap up
That's the thinking and writing of our stretch goal.  Next up would be to allow for all the dogs for owners iwth mutliple ones, and to be able to submit approvals.  The future be so bright, we'll have to wear shades!