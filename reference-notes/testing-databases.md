<!-- Title: Testing Databases -->
<!-- Subtitle: How we can make sure our queries and functions work on Db's! -->

# Why We Test

It is inevitable that our software will stop working for some reason--a person will try to do a thing they normally do and can no longer do it.  Then, they call you and ask you to fix it.

When this happens, you want to isolate what is going on by removing as many variables as possible.  Was it the code, or the database, or the connection, or an errant cord?

By having tests, you can remove the code as a variable in the problem, _or_ isolate which part of the code is presenting the problem.

# Unit Tests Purpose 

'Let's break our code into singular, tiny functions and test each one.  That way we quickly see _what_ isn't working.'

The issue: When we write these unit tests, we need to isolate one piece of code that was not designed to be isolated.


# How We Test
We create a test database which is referred to as an optional argument in each of our functions.  Then, when we can test against that database.

We can use `jest.mock` to test our servers.  This acts as an 'imposter'.  
```js

jest.mock('../db', () => ({
  getUser: (id) => Promise.resolve(
    {id: id, name: 'test user' email: 'test@user.nz'}
 }}}}
 ```
 figure this one out later.  that above code is not right.
 
 


