# Divide & Conquer
## The Tiling Problem

**The Problem:** Given a n by n board where n is of form 2k where k >= 1 (Basically n is a power of 2 with minimum value as 2). The board has one missing cell (of size 1 x 1). Fill the board using L shaped tiles. A L shaped tile is a 2 x 2 square with one cell of size 1×1 missing.

**Example:** Here we have a 4 x 4 grid, with the cell at 2 x 3 missing

![alt text](https://github.com/CameronDeLone/Pics/blob/master/Grid.jpg "Grid")

**Step 1:** We begin by adding an L-shaped tile to fill 3 of the 4 center cells, we can dicide which checking which quadrant has the missing cell (top-left for this example), when we place the L-shaped tile so that we are removing cells from each other quadrant.

![alt text](https://github.com/CameronDeLone/Pics/blob/master/Grid-1Filled.jpg "Grid First Tile")

**Step 2:** Next we take each of the quadants as it's own indiviual problem (*Divide* & Conquer), and repeat the previous step until we reach the base case (a 2 x 2 square, with 1 cell missing).

![alt text](https://github.com/CameronDeLone/Pics/blob/master/Grid-2Filled.jpg "Grid Second Tile")
![alt text](https://github.com/CameronDeLone/Pics/blob/master/Grid-Filled.jpg "Grid Fully Filled")

## Practice Problem:

Assume you have an 8 x 8 grid as shown below, follow the previous steps to fill it out
![alt text](https://github.com/CameronDeLone/Pics/blob/master/8x8-Grid.jpg "8x8 Grid")

## Solution:

To solve this problem we must first follow the steps:

**Step 1:** Split the grid into quadrants                                                                      
![alt text](https://github.com/CameronDeLone/Pics/blob/master/8x8-Grid-Quadrants.jpg "8x8 Grid with Quadrants")

**Step 2:** Place the first L-Shaped tile to remove cells from the 3 quadrants which do not contain the missing cell
![alt text](https://github.com/CameronDeLone/Pics/blob/master/8x8-Grid-Quadrants-1.jpg "8x8 Grid with Quadrants")

**Step 3:** Repeat this process for each quadrant, first splitting it into smaller quadrants, then adding the L-Shaped tile into the 3 quadrants which do not contain a missing cell (cells filled by a previous tile count at *missing*).
![alt text](https://github.com/CameronDeLone/Pics/blob/master/8x8-Grid-Quadrants-2.jpg "8x8 Grid with Quadrants")

Now that we only have 2 x 2 grids (our base-case) left we can fill the remaining cells (this is due to the fact that any 2 x 2 square with 1 missing cell contains exactly 1 L-Shaped set of cells)

![alt text](https://github.com/CameronDeLone/Pics/blob/master/8x8-Grid-Quadrants-Filled.jpg "8x8 Grid with Quadrants")

## Psuedocode:

n = side length of square (always a power of 2 in this case)
p = position of missing tile

Tile(int n, Point p) {
  if n = 2:
    An L-shaped tile fits perfectly in the unused space
  else:
    Determine which quadrant p lies in, and place the L-shaped tile so
    that it lies in every other quadrant i.e. in the center.
    This is always possible because n is always power of 2.

Now each quadrant has one "missing tile". Keep doing the same thing
for each quadrant until the base case is triggered. That is, execute
Tile(n/2, p)
Tile(n/2, p1)
Tile(n/2, p2)
Tile(n/2, p3) 
(where p1, p2, and p3 are the positions of the points comprising the L shape.)

## Final Review

Implement this code to solve for when n = 2^k.

Test for the following values of k: 1, 2, 3, 4
