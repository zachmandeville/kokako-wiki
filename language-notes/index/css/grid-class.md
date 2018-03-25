<!-- TITLE: display:grid -->
<!-- SUBTITLE: Why this grid class is AMAZING -->

# display:grid : so amazing
**display: grid** is a way to quickly map out a grid for your CSS without having to use any framework. and you get to use the cool ass "fr" sizing.

fr is "whatever reaming space"  so for example you could say "display: grid, grid-template-rows: 20px, 20px, 1fr".  Then within this you could put in three div's.  the first div would be 20px, the
second 20px too, the third would fill up the remainder of the grid div.  In this way you can set the sizing within the grid, and use yr classes for each div for their individual margins and padding and colors and not worry about sizes.  It's ridiculously fast!


So let's say you want to have a 2 column site, and the first column is 200px wide.  The second column you don't need to size, you can jsut say "1fr".  Then, if someone is on a 800px screen, that second column will be 600px.  if they on a 1200px screen, it will be 1000px.  

You can also do ratios of 2fr, 1fr and so on, to do more proportional sizing.  

Where i'ma try to use it is on mobile, when I want a header and footer, and then something that takes up the rest.  I can just make a header and footer both be some size like 50px or 3rem, and then the other row be "1fr" and i'm golden!

I think.

update:
yep!  And you can do cool stuff with grid-template-area too, where you give each of your individual divs their own id, then map their placing using grid-template-area.  For an example of this, check zach's js-calculator CSS:

```
.calculator{
  display: grid;
  background-color: #59260d;
  width: 400px;
  height: 600px;
  grid-gap: 10px; 
  grid-template-columns: 1fr 1fr 1fr 1fr;
  grid-template-areas:
  "sc sc sc sc"
  "ac ce dv mu"
  "7  8  9  mi"
  "6  5  4  pl"
  "1  2  3  eq"
  "z  z  pd eq";
  padding: 10px; }
	```
	
	The grid let me essentially draw my calculator in the css file and it worked like a g.d. charm.
	

