# Box Stacking Pseudocode Tutorial

Problem: You are given a set of n types of rectangular 3-D boxes, where the i^th box has height h(i), width w(i) and depth d(i) (all real numbers). You want to create a stack of boxes which is as tall as possible, but you can only stack a box on top of another box if the dimensions of the 2-D base of the lower box are each strictly larger than those of the 2-D base of the higher box. Of course, you can rotate a box so that any side functions as its base. It is also allowable to use multiple instances of the same type of box.

The box stacking problem is best solved using the bottom-up strategy for dynamic programming. Since each box can have multiple instances, we have 3 times the original amount of boxes to consider.

Each box should have four attributes: height, width, depth, and base area.

Below is the psuedocode to implement the solution for the box stacking problem.

```
// the method receive the array of boxes
maxStackHeight(Array boxes):

// First, create an array that has the original box and the two additional rotations of the box

// A box with dimensions (height,width,depth) when rotated becomes (width,height,depth) and (depth,height,width)

// The length of this new array will be length*3

// this will be an array of boxes
Array allBoxes = null;

// Use a loop to first add an original box plus its 2 rotations for all boxes in the boxes array

for (i=0 to n-1):
    // copy original box
    allBoxes.append(boxes[i]);
    // create the first rotation of the box
    Box box1 = (boxes[i].w, boxes[i].h, boxes[i].d, boxes[i].h*boxes[i].d);

    // create the second rotation of the box
    Box box2 = (boxes[i].d, boxes[i].h, boxes[i].w, boxes[i].h*boxes[i].w);

    // append to list
    allBoxes.append(box1);
```
Now the original boxes and the rotations have been added to one list. Sorting the list in dreasing base area is helpful.
```	
// sort allBoxes in decreasing order according to their base area
reverseSort(allBoxes);

	
for (i=1 to n-1):
    for (j=0 to i-1):
	if(boxes[i].w < boxes[j].w and boxes[i].d < boxes[j].d:

```
