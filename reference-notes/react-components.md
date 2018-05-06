<!-- Title: React Components! -->
<!-- Subtitle: Passing things among things ==>


We talked about 'componentDidMount'.  Component Did Mount is giving you an opportunity to do a thing before the componentn is rendered.  It's mounted, but not showing yet.

This comes up when you are making a call to the api, which is done as an asynchronous function.  so you wanna get some widgets, from a server in Petaluma, and then render a page.  Since it's asynchronous, it's going to start that function, and then render the page as it waits...so you never get to see the widgets you grabbed

```
...the state of all the things....

this.saveWidgets = this.saveWidgets.bind(this)
}

componentDidMount () {
  fetchWidgets()
  }
  
fetchWidgets () {
  getWidgets(this.saveWidgets)
}

saveWidgets (err, widgets) {
  this.setState({widgets: widgets})
}

render () {
  return (
    <div>
      <h1>Widgets for the twin!</h1>
      <ul>
      {this.state.widgets.map( () => {
        <li>{widget.name}</li>
	})
      }
      </ul>
   )
 }
```

So here the app would have a state that includes something called widget, which is an array.

When the component did mount, we'll fetch the widgets, and save them to state.

Then, we'll render the page, including the widgets stored in state.  When the state changes, re-rendering is automatically called.   This lets us run an async function _and_ render a page _and_ render it again when the stuff is returned.  With what we have right now, it looks instantaneous---soon we'll likely have a loading screen.


