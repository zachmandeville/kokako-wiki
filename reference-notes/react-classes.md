<!--Title: React Classes -->
<!--Subtitle: Moving from functions to objects -->

# What we talking about?
We are talking about the building blocks of object-oriented programming.  Making objects that will exist in memory, have data attached to them, and will be waiting to come forward when asked.

# Example

```js

import React from 'react'

class App extends React.Component {
  return (
    <h1>React development has begun!</h1>
  )
}

export default App
```

## extends
This says, 'we are making a new Ap object, but we want it to act and work like a React.Component.'


## constructor
```
constructor (props ) {
  super(props)
  }
```

The big difference in moving from functional to object is the concept of state.  Now our components can hold data for themelves.

# A class is a holder of states and functions.

# what this mean

It generally means "self".  It's when the function or thang calls upon itself.
  
