<!-- TITLE: Test Driven Development Overview -->
<!-- SUBTITLE: A quick summary of Test Driven Development Overview -->

# Background

Test-Driven Development style of development where you write tests as you code, as the proof that your code works.  So you can write the test of what it is you'd like to do, or think should, then write your code to pass that test.

# The Parts of a Test

## Arrange

Setting up the variables and data that are needed for the test.  this could be variables you are
passing into the test, or the expected output.

##  Act

The space in which you run your function.  You _do your thing_.  This doing of the thing is called
actual.

## Assert

You set the conditions for fail or pass.  It shows itself often as:

`expect(actual).toEqual(expected)`

# Requirements to Run a test

* A package.json
  * 'jest' dependencies
* To create a package.json: yarn init -y
* To install jest in yr directory: yarn install jest
  * This will add all the jest modules into yoru node_modules folder and add jest as a dependencie
    in yr package.json
* In your package.json add, in the scripts section: "test: "jest"
* test/tests
  * file-name.test.js  for each of your tests 

# Tricks within the Test Script

If you wrote a bunch of tests in a file, but now wanna run just one, you can do so by appending that
test with only, eg:

`test.only(the test you wanna run)`


You can also do it the other way, if there are tests you _dont'_ wanna run, by using test.skip:
`test.skip(theTestIWannaSkip)`

Using test.skip on multiple lets you choose just the select few you wanna run at a time.

# Console Logs
You can write your code with console logs, when running through a loop, to return each iterations
running score.  This way, if there is an issue you can run through the console and see where the
error occurred.
