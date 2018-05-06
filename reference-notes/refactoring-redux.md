<!--Title: Refactoring Redux -->

# Steps of refactoring the wombat-redux exercise.

## Create a new File, called reducer

import it into index.js
bring all your reducer functinos over to there.

## create 'action creator functions'
- create action.js

```
function deleteWombat(wombat, event) {
  store.dispatch({
    type: "DEL_WOMBAT",
    wombat: wombat
    })
    }
```

Becomes:

```
function deleteWombat(wombat,event) {
  let action = actions.delWombat(wombat)
  store.dispatch(action(wombat))
```

And in our action.js file, something like this:

```
function delWombat(wombat) {
  return {
    type: 'DEL_WOMBAT',
    wombat: wombat
    }
}
```

This lets us separate our actions from what calls them, which also makes it easier to make sure we don't have typos in where we call it.  It also helps us test the actions themselves.  And it brings us down to that sweet '4 line function' state.  Or: the ideal state.



