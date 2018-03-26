<!-- Title: Routes -->
<!-- Handling them get and pull requests on yr javascript app -->

# Background

When someone accesses a website, they are (most often) sending a GET request to the server.  The server needs to know what to do _with_ that GET request.

Similarly, if someone is sending a POST request (e.g. sending info through a form), then the server needs to know what to do with that request.  Routing is a way to handle these requests and route them to the right pages/actions.

# Basic Example

```js
server.get('/', function (req, res) {
   res.send('hi')
   }
```
This is saying "when the server gets a request to the root of the website (website.com), then run the function that displays hi to the user.  

You can also expand the 'hi' there to be an entire file...e.g.

```js
server.get('/', function (req, res) {
   res.send(__dirname, '/index.html')
   }
```
Or, "When the server gets a request to the root of the website, send the visitor my index.html page, styled to be my homepage.

# Dynamic and Static

In the above example, we are sending a static webpage.  index.html is an unchanging file.  This means you can't personalize that page though, based on the visitor.  What if you wanted a 'Hey visitor!' at the top of that index.html page?

For this, you'd use 'views' and 'templates'.  You can load a template index.html file with sections for variables like 'name' or whatever else.  Then when someone sends a get request, they are given their specific view.

**For Views, you'd use res.render() instead of res.send()**

# Handlebars
(link to its own page: [handlebars](javascript/handlebars)
A templating library from nmp.  Named such cos you use a bunch of brackets that look like handlebar mustaches.

# Templates
The thing to remember with templates is that they are _the melding of two worlds_.  They are combinding the templating code with basic html.  So you can still offer the structure and styling of html/css, but personalized based on the template language.
