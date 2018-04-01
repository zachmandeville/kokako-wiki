<!-- Title: Super Test -->
<!-- Test that HTTP! -->

# Purpose
Provides a fantastic tool for testing http (receiving and sending messeages from your server)

# How it Works

It makes a request to your server, with a set expectation.  You can then decide what that expecation should be. So it's following the same **Arrange, Act, Assert** method.

It's an npm module, so it can be installed to your app directory (or repo) with `yarn add supertest`

# Example

```html
const request = require('supertest');
const express = require('express');
 
const app = express();
 
app.get('/user', function(req, res) {
  res.status(200).json({ name: 'tobi' });
});
 
request(app)
  .get('/user')
  .expect('Content-Type', /json/)
  .expect('Content-Length', '16')
  .expect(200)
  .end(function(err, res) {
    if (err) throw err;
  });
```
When you are doing these requests, you have to think like the test is the browser sending a request to the server, and expecitng a certain response back.  In this example, our function is to receive a request and send back a json object and the status 200 (or 'Okay!')

So the request function is saying, line by line:
Run get to the route '/user'
expect to receive a JSON back
Expect that to be 16 characters (including the spaces and curly braces)
expect the server to say "yep! you go tthe request okay!
End the test and if there's an error, throw it!


# Cool Tips

* When testing handlebar templates, to make sure the data is right, you want to use .trim for the text request.  Otherwise, the handlebar could be putting in unintentional whitespace that'll mess up your tests.

* when running a get request, youc an have `.query` and then pass what is being queried as an object, i.e `name: harrison` instead of having to type `?name=harrison`

* `console.log(res,text)` Will log to the console your html...as that is marked as TEXT in the http being transferred.

