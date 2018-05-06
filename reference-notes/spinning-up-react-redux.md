<!--Title: Spinning up React-Redux -->

Needs:

Store,
Action,
Reducer

Import {createStore} from redux
import {Provider} from 'react-redux'

in index.js:

```
const store = createStore(reducers)
<Provider store={store}>
<App />
</Provider>
```

from now on, the only way we pass data to components is through props.  

## Connect
import {connect} from 'react-redux'
export default connect()(App)


## Key Concepts!

Components know longer are creating their own states.  Redux holds the state, and dispatches changes to the compontents through props.  So the components are deciding how to display the current state, but Redux is the one deciding the state.

There is now one big STORE that holds the state, which is being determined by Redux.   The store is created in the client/index.js page  through the createStore function.

You provide the store to all the components through the index.js page rendering, by using <Provider store={store}>
