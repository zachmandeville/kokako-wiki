<!-- Title: Heroku Overview -->
<!-- Subtitle: An Overview of, you guessed it, Heroku! -->

# What it is!
https://heroku.com

Heroku helps you deploy your app so it is accessible to the larger world.  So far we've been making apps that run on our local device.  With Heroku, we can run our servers and apps but accessible from a browser anywhere.

# Why we use Heroku
- Fairly Simple to use.
- You can host 5 sites with them _for freeeeee_.

# Using Heroku

## Command Line Tool
There is a command line tool that helps you check on your site, and offers many useful commands!
You can install it here: https://devcenter.heroku.com/articles/heroku-cli

### Useful Command line tool commands

`heroku apps`
Will list all the apps you have hosted on heroku

`heroku create {name of your app}`
Will create a new app, hosted on heroku at name-of-your-app.herokuapp.com

`heroku logs`
Will list the logs on your server (so if you entered console.logs they'd appear here)

## Pushing to Heroku

This works much like github, but there is only a master branch (it'll accept other branches, but they don't do anything).  To push to heroku, from your specific branch, you'd use:

`git push heroku <your-branch-name>:master

## Configureing yr code so it works with heroku
### package.json
Heroku runs your start script, so whatever you put there is what heroku will run. (this is found within your scripts section up top.)  It should be start: node index

### index.js

In your index.js you assign the port your server is available on.  So far, our index.js file looks like this:
```js
var server = require('./server')

var PORT = 3000 \\this is the port the server is listening on"

server.listen(PORT, function () {
  console.log('server is listening on port ' + PORT) \\see, i told ya
  })
```

We are interested in the `var PORT` section.  For heroku, change it to.

`var PORT = process.env.PORT || 3000`

Which is saying "look at whatever port is set on the service i'm deployed on(heroku).  OR, if that's not available, use 3000". 


