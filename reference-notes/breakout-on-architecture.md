<!--Title: Breakout Session on Architecture -->

# Topics

## Fit Puzzle Pieces
- Think in the context, "we are not going to get this right from the start, so let's get things wrong as soon as possible."
- Don't design the whole visuals of the app, then try to build them all, cos you'll find as you build them the design was wrong.
- **general rule** smaller the better will always serve you.
## Breaking an app down to parts
- How little of this application can I build right now?
- Look at the mvp and think, "what do these all have in common?  What are non-negotiables do they all need?  How little of these foundational things can I build, to demonstrate I'm ready to build new things."
- Building a stack: get the minimum amount going all the way through the whole stack and deliverable to the customer.  
- There are types of apps that are 'big risks', where you can't deliver a smaller version _without_ buidling the whole version, where everything is so interlocked in the mvp that the smallest part is actually quite large.  In that case, start to think of contingencies...and ways to build out the stages to make sure each section is working without having it be deliverable _yet_.
- **'Be the app, so you can notice the data flow of the app.'**
## Foundations
- Start by writing the API, so you can start to map out the app and data flow.  With a clear api, you can build really the entire app as you understand the central contracts of it.
- Defining the API:
  - What are the Routes?  What are the requests for these routes?
  - In other words: what are you passing, and what are you receiving, and what does it look like when you _can't_ get what you want.
  - What are the responses?  What do they look like?  Is there other info that's coming in?
- Start making screens, so you can prove that you are providing data up to the screen.  The code of the screen will change, but regardless of design data will need to be served up to it.  By building something simple, you can confirm that you are serving something up all the way to the client.
- In terms of dividing tasks, it makes sense for one person/partner to build a sliver of the entire stack, from client to api to routes to db.  By confirming that the full stack works, others can build off that sliver by pattern matching what has been made.
- And also, start testing at this point.  Best place to start is routes, where you are testing at least in postman if you aint' doing a full test suite yet.
- Also, be clear on your names for someone after to be able to understand the logic _based_ on the name. 

## What Order to Start
- Define a small, useful documentation for API.  Doesn't need to be complete (it won't be complete), but it gives people somewhere tos tart from.
- Build out the routes and db based on a sliver of that api, to make sure the three parts are working.  Test this to ensure.
- Build out the client api.js (v. similar to the db section,)  this is the client to the server, essentially, and you wana make sure the requests that yr getting for the api are something that the client can render.
- Design a simple screen to confirm that the whole stack is working, from a client request, to pinging the server through the API, that returns a response that is being rendered on the client.  The design of this will change, but yr confirming that the concept now works.
- After you've agreed upon the API, you can agree upon the state.  "Once I've defined that there is a meeting API, I can assume that there'll be some concept of meetings that the app should know about, in other words that meetings will exist in some way in the state."   So when that happens, define the state!
## API: How, What, When
## State?
## Plan v. Wing: How much to plan, and how much to figure out on the fly.
- We need to get used to the idea of building something you will rip out later.  You are building on working assumptions of how things _should_ operate, and then as your knowledge changes, you'd change those assumptions nad api.
- It's  not until you start working on a problem that you realize that you didn't understand the problem.
- As you start to work on a new feature, that would change the state in some way, the best process is to make a branch and test that new feature on your own understanding.  and _then_ add it to the rEADME (before working further, or merging to master).  This signals to everyone else that you've thought about this new feature and how it should work, and let them be able to prepare for this feature being merged (prepare possibly by giving feedback to help your own understanding). 

