<!-- TITLE: Setting Up Node Server On Heroku -->
<!-- SUBTITLE: The steps from empty directory to working app! -->

# Make sure you have all the tools you need
You need git, node, and yarn.  You can check whether you have them on your computer using:
`git --version`
`node --version`
`yarn --version`
Each of these should return a version number, _if_ you have the the tool installed on your computer.  If not, you'll need to search, download, and install each one.

# Make a new directory and initialize git within it.
`mkdir mycoolapp && cd mycoolapp`  This means "make directory called mycoolapp AND change directories into this one.
`git init` This will initialize an empty git repo here.

# Header# Make sure you have all the dependencies

* initialize this as a node app with `yarn init -y`
	* This will create a package.json file connected to our github repo.
* Install the yarn dependencies
	* jest and supertest and cheerio for testing
	* nodemon for debugging.
	* express for server
	* express-handlebars for templating
	* body-parser for middleware

* Add scripts for testing and starting the server:
```js
  "scripts": {
    "debug": "nodemon --inspect index --ignore data.json",
    "test": "jest --watch --noStackTrace",
    "start": "node index"
}
```

"debug" nodemon means when we run 'yarn debug' , it'll use nodemon
'test" just means we'll use jest.  the two additional flags are so the tests continually run.
"start" means when we do 'yarn start' it starts it up using just straight up node.

# Create an index.js file
This will spin up the server we define in our server.js page

It should like like so:
```js
var PORT = process.env.PORT || 3000

server.listen(PORT, function () {
  console.log('server is listening on port ' + PORT) \\see, i told ya
  })

```

# Create a server.js file
This will be the one that actually says 'hello world'

Should look like this:
```js
var express = require('express') // Use express for server
var hbs = require('express-handlebars') //Use handlebars for our templating
var bodyParser = require('body-parser') //?? I think it's used for handlebar

var server = express()

// Middleware-- don't fully know what this means.
server.engine('hbs', hbs({
  defaultLayout: 'main',
  extname: 'hbs'
}))

server.set('view engine', 'hbs')
server.use(express.static('public'))
server.use(bodyParser.urlencoded({ extended: false }))

server.get('/', function (req,res) {
  res.send('hello world!')
})

module.exports = server
```

# Test it locally
`yarn start` should start up a server at localhost:3000 and it should say 'hello world'.


# Do that heroku stuff.
Follow the instructions on our [heroku page](http://kokako.solarpunk.cool:3000/heroku-overview) 
## Push to github (to make sure all recent changes are on your remote git repo)
## create a heroku app
## push with git with `git push heroku <branchname>:master`