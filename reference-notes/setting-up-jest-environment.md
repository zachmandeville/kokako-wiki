<!-- TITLE: Setting Up Jest Environment -->
<!-- SUBTITLE: A quick summary of Setting Up Jest Environment -->

# Installing necessary things.
`yarn add jest` To add the Jest dependency.  Jest runs all the tests.

`yarn add superagent` This is an addition of sorts to Jest, that allows the test to pretend to be a browser, sending requests to your server.  It is often shwon in your code as: `request = requires('superagent')`

`yarn add cheerio` This is if you need to parse the text of html to check whether certain strings are present. It's the node version of Jquery essentially.

# Set up your tests folder.
Jest knows to look within a folder called tests for all your tests.  They should be written as `testname.test.js`

# The Structure of a jest test function
## Simple test
```js

test('purpose of test', function(){
//Arrange
  expected = 'Hi'
//Act
	actual = 'Hi'
//Assert
  expect(actual).toequal(expected)
	})
	```
	This follows our AAA test design.  You _arrange_ the variables necessary for a test, then provide an _action_ (the function being run that produces a value) and an _assertion_ (that the function produces a value that equals your expected value).
	
	


