<!--Title: Redux Overview -->

# Wordcloud of what Redux is
Broadcasting, a radio instead of gossip.  A teacher in front of students.  Instead of there being many states within each class, there is now one global version of state.

#Key Terms
##State
The state of the app, what we've seen before-but now for the entire app instead of objects.
##Store
Where the state is stored.
##Reducer
A function that can change the state.

# Random Thoughts
- We use switch statements intead of if statments, that are listening to events for when something like 'ADD_WOMBAT' or 'DEL_WOMBAT' happens.  It's a cleaner method, espec. since many of these are just doing a single thing after.
- Spread is awesome.  It brings in an array within another array.  Good to remember [What we know about spread](/language-notes/spread)
- `store.subscribe` -- When you create a store (which is aware of the state and the actions that can be done upon it), you want to add an event listener that subscribes to the store.  This means that whenever any action happens to the store, the event listener is aware and does a thing.  Mostoften, that thing is 'render', as it'll render the page again with the new state.

