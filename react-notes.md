<!-- TITLE: React Notes -->
<!-- SUBTITLE: A quick summary of React Notes -->

# Header

## webpack
bundle.js

entry :
output:
package.json
srcipt { "start": "node server & webpack --watch"}

## react
JSX is the javascript markup 

This is required in HTML
```text
<div id=root> < /div>

<script src=bundle.js></script>
```

This is my index.js
```text
var react = require('react') 
var reqiure react-dom


function MyComponent(data) {
  var name = data.name + ' from EDA'
  return (
        <div>
        <h1> Hi There {name}<h1>
        <MyOtherComponent/>
        </div>
}

var data ={name:harrison}
var view = MyComponent(data)

function MyOtherComponent(data){
	return(
	<p> this is the content of the page </p>

var placeToMount = document.getElementById('root')

ReactDOM.render(view, placeToMount)
```


## map over array with react
require data 
pass data into function with (props)
then run your map function

```    {props.recentEntries.map (function (entry) {
            return <li><a href={entry.link}><h2>{entry.name}</h2></a></li>})```