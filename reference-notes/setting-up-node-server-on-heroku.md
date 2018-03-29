<!-- TITLE: Setting Up Node Server On Heroku -->
<!-- SUBTITLE: The steps from empty directory to working app! -->

# Make sure you have all the tools you need
You need git, node, and yarn.  You can check whether you have them on your computer using:
`git --version`
`node --version`
`yarn --version`
Each of these should return a version number, _if_ you have the the tool installed on your computer.  If not, you'll need to search, download, and install each one.

# Make a new git repo and clone it to yr computer
This can be empty, we just want the directory to be a _git_ directory
So make it on github then do:
`git clone https://github.com/myname/mycoolapp.git`
`cd mycoolapp`

# initialize your repo as a _node_ repo
Run `yarn init -y` within your repo.  This initializes all the things you need for node like a package.json and a yarn.lock file... the -y just says 'yes' to all the default things yarn would ask during the usual init.
# Make sure you have all the dependencies installed
### Dependencies for running tests
`yarn add jest` our testing module.
`yarn add supertest` this works with jest so that we can test http responses
`yarn add cheerio` for parsing the html requests like they jquery.
`yarn add nodemon` so you can debug code by making changes while the server is running and hot reloading it. (instead of having to turn off and on your server to see the change.

### Dependencies for spinning up that server
`yarn add express` .  Express is our server module.
`yarn add express-handlebars` this adds the ability to use handlebar templating with express.
`yarn add body-parser` this is necessary for the middleware that makes handlebar function (you'll see it in the server.js file later on in this apge.)

# Edit your package.json to use your cool modules.
Within your top app object add a scripts object, it'd look like so:
```js
  "scripts": {
    "debug": "nodemon --inspect index --ignore data.json",
    "test": "jest --watch --noStackTrace",
    "start": "node index"
}
```

The three scripts do the following:

`"debug": "nodemon --inspect index --ignore data.json"` we run 'yarn debug' , it'll use nodemon to start the server.  For everything else, we just use node.
`"test": "jest --watch --noStackTrace"` just means we'll use jest.  the two additional flags are so the tests continually run.
`"start": "node index"` means when we do 'yarn start' it starts it up using just straight up node (as compared to yarn debug).
# Create an index.js file
This determines what port will be used when  you run yarn start.  For Heroku, it important that you set the port variable with process.env.PORT || 3000.  This lets heroku use whichever port it needs to, or if you're not using heroku(like running this on a local server) it'll use 3000.

The script would look like so:

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

//When the server receives a request for the home directory ('/'), then send back 'hello world' as the response.
server.get('/', function (req,res) { /
  res.send('hello world!')
})

module.exports = server
```

# Test it locally
`yarn start` should start up a server at localhost:3000 and it should say 'hello world'.


# Get it on Heroku
## Download and install heroku on your local machine.
Follow the instructions on our [heroku page](http://kokako.solarpunk.cool:3000/heroku-overview) 
## Push to github (to make sure all recent changes are on your remote git repo)
Go through the ritual of adding, commiting, and pushing to github so that index and server file and all that are added to your repo.
## create a heroku app
Inside your repo invoke the command `heroku create {nameOfApp}`  This will make a new app on heroku for you available at the address nameOfApp.herokuapp.com
## push your repo up to Heroku
You can do this with git, actually, by invoking the following command when in your directory: `git push heroku <branchname>:master`.  This pushes whatever content is at the branch you specified up to heroku.