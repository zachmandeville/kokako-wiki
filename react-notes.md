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
This is required in HTML
```text
<div id=root> < /div>

<script src=bundle.js></script>
```

This is my index.js
```text
var react = require('react') 
var reqiure react-dom


function myTemplate(data) {
  var name = data.name + ' from EDA'
  return (
        <div>
        <h1> Hi There {name}<h1>
        <p> this is the content of the page</p>
        </div>
}

var data ={name:harrison}
var view = myTemplate(data)


var placeToMount = document.getElementById('root')

ReactDOM.render(view, placeToMount)
```
