<!-- TITLE: While Loops -->
<!-- SUBTITLE: Doing a thing for as long as you need -->

# Usage
Run through a loop for as long as a condition is true.  This could mean the loop runs forever.  It's
useful for making sure the entirety of changes you wnat to make do change, and not just that an
action went for a certain number of loops (like it would for a straight for loop)

# Example

For example: I wanted to turn a certain number of cells into mines in my minesweeper game. Depending
on board size, it should create a set amount of mines.  I did this by running random cells and
changing their property isMine to true.  Initially I did this with a for loop saying:
`(var i = 0; i < maxBombs, i++)`
And so it would run throuch the loop for as long as the max bomb size. the problem was that it would
choose the same cell every now and then, which would make the ultimate number of bombs less than the
maxbomb size.  I didn't want this--I wanted to run through the loops until the maxbomb size was
reached.  In this case, a while loop was perfect.

```javascript

function makeBombs(maxBomb){
//Turn a random assortment of cells into mines, by marking isMine to true.
//The number of mines is defined with variable maxBomb
    var numBombs = 0;
    while (numBombs < maxBomb) {
	var cell = board.cells[randomize()];
	if (cell.isMine)
	    continue;

	cell.isMine = true;
	numBombs += 1;
    }
}
```

So I can declare a variable, that acts as a running count for bombs.  While this number is < maxBomb
count...i keep running through the loop.  If the loop finds a cell that's already a mine, it
continues onto the next cell (continue means "start up at the top of the loop again!".  If it finds
one that _isn't_ a mine, it sets it's isMine to be true and then tallies up the bomb count.  In this
way, the bomb count keeps being tallied until it reaches the max bomb size, and I can confirm that
it'll always have as many bombs as the maxBomb number.  Very good.  Very cool.
