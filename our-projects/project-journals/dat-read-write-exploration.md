<!--Title: Exploring how Read and Write works on DAT -->
<!--Subtitle: Part of Zach's personal project of working on a DAT app! -->

# Prerequisites

This site requires Beaker Browser to run.  It is made using DAT://, which only has support on Beaker.  The browser  itself is the server in which it runs.

You can find my version (and fork it if you want!) here: dat://4b9b475826314432f930122835130f298c4e333ad104a237e6ff38195334ffd1/

# Directory Structure

There are 7 files in this site directory:

`.datignore`: This is similar to a .gitignore file.  Since dat is uploading a folder from your computer, then you may end up uploading temporary files or system files.  You can indicate which ones you want to ignore in the upload here.

`dat.json`: This handles the name of the dat site.  It doesn't seem to be much more.  The entirety of this .json is here:
```json
{
  "url": "dat://5d382324488d33d2a1c808fbe33a1fe586701c2bb9dd31b570a76e6c251cab2c/",
  "title": "Read&Write",
  "description": ""
}
```
In other words, the url of my site.  The title of it, and a description if entered.

`index.html`: This is the only page on this site.  It's an html page, but with functions attached to the onclick events.  The page is made up of two input areas where you can either enter a color and change the background color, or fetch a site and change the bg color _of that site_.  We'll look at it in more depth below!

`local.json`: This json has a single entry for color.  So the script must say to pull the bg color from yr local.json.  And so when you enter in a new color, it updates the local.json.

`scriptjs`: This handles all the functions that can occur within the site.  We'll cover it in more detail below.

`SpaceMono-Regular.ttf`: A font file.  Makes the site look nice.  It makes me wonder if we could change the font-family in the same way we change the background color.

`style.css`: Handles the styling of the page. Nothing more really.  

# Deep dive into the index.html file!

```html
<html>
    <head>
        <title>[r&w] read&write with beaker and dat</title>
        <meta charset="utf-8">
        <script src="/script.js" type="text/javascript"> </script>
        <link rel="stylesheet" href="/style.css">
	<!-- We got all your basics in here. Nothing fancy yet! -->
    </head>
    <body>
      <!--The entire site, essentially, is a modest grid with a couple input areas -->
        <div id="grid-container">
            <h1 id="title">reading and writing dats</h1>
            <input onkeydown="enter(event)" id="color-input" placeholder="#f2f2f2">
	    <!-- An input field with the id 'color-input'.  It has a sample color to get you
       started.  onkeydown='enter(event)' is referencing a function in our script.js file.  So when
	    the site senses a keyboard button pressed, it runs the enter function.-->
            <div></div>
            <button onclick="save()" id="save-btn">save</button>
	    <!-- Similar to the enter(event) above.  When the save button is pressed, it runs the
       save function.  -->
            <input onkeydown="enter(event)" id="dat-input" placeholder="dat:// to read">
	    <!-- Same as enter(event) above, but for an input field with the id of dat-input. -->
            <div></div>
            <button onclick="fetch()" id="fetch-btn">fetch</button>
	    <!-- When this button is pressed, call the fetch() command. -->
        </div>
    </body>
</html>
```

## Deepdive into script.js

```js
//Listen to the document(webpage).  When the entire content has loaded, run the setColor function,
//and pass along as the argument whatever the 'host' url is. 
document.addEventListener("DOMContentLoaded", function() {
    setColor(window.location.host)
})
//window.location.host is a fundamental JS element that is equal to the domain url.  So the
//window.location.host of coolguy.website/coolshit would be coolguy.website.  The
//window.location.url of a dat site would be the full path of that site.
//in other words, set the color based on what's found at this specific dat site.

function setColor(url) {
    // open the dat archive
    var archive = new DatArchive(url)
    //new DatArchive(url) is a function of dat's web api.  It creates a new archive instance of
  //whatever dat archive you sent it.  The archive, as I understand it, is the entire directory of a
  //particular site (like it's dat.json and script.js and all that.)
    try {// to fetch a file from the archive
        archive.readFile("local.json").then((contents) => {
	//Above is another web api function (and a promise!).  In this new instance we made, read the local.json file, then do the following with the contents:
            var color = JSON.parse(contents).color
	  //set a new variable called 'color' that is set to whatever we can parse in the color
	  //value in that local.json.
            document.body.style.backgroundColor = color
	  //in our current site, create a style attribute for backgroundColor and set it to whatever
	  //we grabbed in that local.json file.
        })
    } catch (e) {
      //Catch an error if there's an error and show it in the console.
        console.error(e)
    }
}
//In Summary: the color is set to whatever hexcode color value is currently in the local.json of this site(or
//dat archive).  

//This function saves our input color value and changes the current dat to reflect this!
function save() {
    var colorValue = getInput("color-input")
  //create a variable called colorValue that is equal to whatever is in our input tag with the id
  //'color-value'.  The getInput function is defined below.
    document.body.style.backgroundColor = colorValue
    //set the current sites background color to whatever that colorValue is.
    var archive = new DatArchive(window.location.host)
  //create a new instance of our datArchive
    archive.writeFile("local.json", JSON.stringify({color: colorValue}, null, 2)) 
  //update the local.json file with that input color value.  This makes it so that the next time we
  //load the site up, it still has our older color.
  //JSON.stringify is a fundamental function.  the first argument takes what it is we are writing,
  //the second and third are to help with the spacing in that object.  I don't fullly get that last
  //part, but essentially 'null,2' makes the spacing nice in that local.json object.
}

//When the user presses enter on either of the fields, figure out where they pressed enter and run
//the necessary function.
function enter(e) {
    if (e.key == "Enter") {//if they pressed the enter key, then...
      //check if they prssed it while in the color-input input area.  
        if (e.target.id === "color-input") {
	  //if so, run the save function.
            save()
        } else if (e.target.id === "dat-input") {
	  //else, if it was in the dat-input function, run our fetch command (defined below)
            fetch()
        }
    }
}

//Grab the URL of any archive site.  If that datARchive has a local.json with a color key, then
//we'll change the color of our site to match this one.
function fetch() {
    var url = getInput("dat-input")
    setColor(url)
}

//Grab the contents of whatever is in the input field and return it.
function getInput(name) {
    var input = document.getElementById(name)
    //set a new variable called input to be whatever element in the DOM has the name that we passed.
    var val = input.value
    //create a new variable called val that is set to whatever is the value (in this case the text)
  //that's inside that input area.
    input.value = ""
  //reset the value of the input field (so the text we entered disappears, knowing it was entered.
    return val
  //return whatever the value we set was.
}
```




