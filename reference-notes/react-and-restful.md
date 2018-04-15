<!--Title: React and REST -->
<!--Subtitle:  The importance of State -->

Psych!  This is really a talk about API

#Basic Def of API
It's a common way for two languages to talk to each other.   It's like pidgin in the web.
It's a return to the concept of CRUD(create, read, update, delete).  

The purpose of our talks this week will be, "How can we leave the presentation alone and just focus on the data?"

#HTTP Verbs

GET- read
POST- create
PUT/PATCH- update
DELETE- delete

(**Small side note about put and patch:**  Originally, put was for updating the entire thing.  Patch, then, was only for updating a certain part of information.   Be v. careful when consuming API's to learn how their updates work, cos they can vary on their definitions on these two thangs.)

## Example

Let's say I got a site with a bunch of users.  Now I wanna look up all the users.

I'd run a `GET` request on `/users`.
I'd also want a route for a `GET` request on `/users/:id`, to look at a specific user.

If I wanted to make a new user, i'd have a `POST` request for `/users/`

If I wanted to update the details of a user, I'd create a `PUT` request for `/users/:id`

And if I wanted to delete a user, I'd create a `DELETE` request for `/users/:id`

These are conventions.  You don't _have_ to follow it, but it makes interacting and collaborating with others much easier.  The point of an API is to give someone else access to your system, and so you want to make that as clear and easy as possible.

#JSON

javascript object notation.  It's a markup language/encoding language for passing data to different apps.

Deceptively similar to regular js object.  For example, here's a regular JS object:
```js
{
user: {
  id: 587,
  name: charlie,
  color: orange
  }
}
```

Here that is as JSON:
```js
{
"user": {
  "id": "587",
  "name": "charlie",
  "color": "orange"
  }
}
```

The quotes are important, and point to what JSON's point is.  JSON turns complex javascript objects into strings.  HTTP understands strings, it doesn't understand complex objects.  So json makes data more easily accessible to http requests.

# Changing how we write up our sites, for API!

When you spinning up an express server, and you want to use JSON and API's, you'll want to add

`server.use(express.json())`

Also, instead of doing `res.render` or `res.send` as the responses to `GET` requests, you'll use `res.json`

#Postman
A way to navigate and test API's

# checking api on the command line
`curl -X GET https://site.com/people`
or
`curl -X POST https://site.com/people`



