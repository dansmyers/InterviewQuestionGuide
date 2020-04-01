# Divide & Conquer
## The Tiling Problem

**The Problem:** Given a n by n board where n is of form 2k where k >= 1 (Basically n is a power of 2 with minimum value as 2). The board has one missing cell (of size 1 x 1). Fill the board using L shaped tiles. A L shaped tile is a 2 x 2 square with one cell of size 1×1 missing.

**Example:** Here we have a 4 x 4 grid, with the cell at 2 x 3 missing

![alt text](https://github.com/CameronDeLone/Pics/blob/master/Grid.jpg "Grid")

**Step 1:** We begin by adding an L-shaped tile to fill 3 of the 4 center cells, we can dicide which checking which quadrant has the missing cell (top-left for this example), when we place the L-shaped tile so that we are removing cells from each other quadrant.

![alt text](https://github.com/CameronDeLone/Pics/blob/master/Grid-1Filled.jpg "Grid First Tile")

**Step 2:** Next we take each of the quadants as it's own indiviual problem (*Divide* & Conquer), and preform the previous step again.

![alt text](https://github.com/CameronDeLone/Pics/blob/master/Grid-2Filled.jpg "Grid Second Tile")
