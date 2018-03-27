# Make a New Directory
# Git Init
# set up node in this repo
`npm init -y` initialize node in this repo and say Yes! to all questions
this makes a package.json file
# Install Express
# Set up yr index.js file (we also use server.js)
```js
const express = require('express')
const server = express()

server.listen(2525)

server.get('/',function (req,res) {
  console.log('server be saying hi')
  res.send('Hi!')
  }
```
