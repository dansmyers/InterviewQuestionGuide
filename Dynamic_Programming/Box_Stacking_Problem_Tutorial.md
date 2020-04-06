# Box Stacking Problem

## The Problem (As given on Geeks for Geeks):

  You are given a set of n types of rectangular 3-D boxes, where the i^th box has height h(i), width w(i) and depth d(i) (all real numbers). You want to create a stack of boxes which is as tall as possible, but you can only stack a box on top of another box if the dimensions of the 2-D base of the lower box are each strictly larger than those of the 2-D base of the higher box. Of course, you can rotate a box so that any side functions as its base. It is also allowable to use multiple instances of the same type of box.
  
## How to Make Sense of It:

  In this problem there are n types of 3 dimensional boxes. As such, each type of box can be rotated to form three unique instances of itself, each with its own length, width and height. For this fact, a set of n types of boxes leaves us with 3n ways to add a box of that type to the stack. In other words, we can generate 3n boxes from the n types of boxes available for stacking.
  
  In order to find the height tallest possible stack from these boxes, we must break our problem down into subproblems with optimal structures. To do so, a good first decision would be to choose a box to represent the top of the stack, and then work our way down. This creates the following recursive relationship for maximum stack height (MH): The maximum stack height for a stack with box b at the top is the height of box b itself, plus the maximum possible stack height generated using only boxes that fit underneath box b in the stack.
  
  In order to solve this problem dynamically, we need to recognize that for one box b to fit legally beneath any other, it must have strictly larger length and width dimensions, and thus a larger base area (length(b) * width(b) > length(other) * width(other)). Also, the boxes with the largest base areas will have a tendency to be the top of relatively small stacks, and to be underneath top boxes with smaller base areas in the more optimal stacks. Because of this, it is useful to sort all of the 3n boxes we have generated in decreasing order of their base areas. Once we have done so, the recursive relationship can be formally expressed MH(b) = Max(MH(c)) + height(b) where b represents our choice for the top box and c represents any box that can go underneath b. 
  
  From here, we have all the information we need to design and implement an efficient algorithm. We will start with the list of all of our boxes in decreasing order of base area, paired with their respective maximum stack heights. Initially, we will set all the maximum stack heights to the heights of the boxes they correspond to, but most will be updated as we complete the problem. In order to complete the problem effctively, we will need to traverse the list from left to right, comparing each box b to all boxes to the right of b, in order to determine whether or not those boxes will fit on top of b. Whenever we discover such a box, we wil update the maximum stack height of this newly discovered box e. This will be done by replacing the MH(e) with the maximum of MH(e), and MH(e) + height(e). Doing this prevents us from having to go back and reconsider the height of any box that might might fit underneath b, since the MH(b) will already be determined by the time we reach b in our traversal. On the whole, this operation will end up being O(n^2), which is way more effficient than brute force. 

# Box Stacking Pseudocode Tutorial

Problem: *You are given a set of n types of rectangular 3-D boxes, where the i^th box has height h(i), width w(i) and depth d(i) (all real numbers). You want to create a stack of boxes which is as tall as possible, but you can only stack a box on top of another box if the dimensions of the 2-D base of the lower box are each strictly larger than those of the 2-D base of the higher box. Of course, you can rotate a box so that any side functions as its base. It is also allowable to use multiple instances of the same type of box.*

The box stacking problem is best solved using the bottom-up strategy for dynamic programming. Since each box can have multiple instances, we have 3 times the original amount of boxes to consider.

Each box should have four attributes: height, width, depth, and base area.

Below is the psuedocode to implement the solution for the box stacking problem.

```
// the method receives the array of boxes
int maxStackHeight(Array boxes):

	// keep track of the size of the boxes array
	int n = boxes.size();
```
First, create an array that has the original box and the two additional rotations of the box. A box with dimensions (height,width,depth) when rotated becomes (width,height,depth) and (depth,height,width). The length of this new array will be n*3.
```
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
		allBoxes.append(box2);
```
Now the original boxes and the rotations have been added to one list. Sorting the list in decreasing base area is helpful. This makes implementing the bottom-up approach much more straight forward. A box with a larger base area cannot be placed on one with smaller base area.
```	
	// sort allBoxes in decreasing order according to their base area
	reverseSort(allBoxes);
	
	// update n to reflect the size of allBoxes
	n = n*3;

	// create a new array to hold the maximum possible stack height for all indexes in allBoxes
	int[] maxStackHeight = int[n];

	// to start, fill every entry with the height of the box at that index
	for (i=0 to n-1):
		maxStackHeight[i] = allBoxes[i].h;

	// compute maxStackHeight values using the bottom up stategy
	// By the end, one of the indicies will be the true maximum stack height
	for (i=1 to n-1):
		for (j=0 to i-1):
		
			// check if box j has a larger base than box i
			if(allBoxes[i].w < allBoxes[j].w and allBoxes[i].d < allBoxes[j].d:
			
				// Box i is smaller than box j and box i can be added to the maxStackHieght[j]
				// Only do this if this yields a larger result than maxStackHeight[i]
				// This means that certain indexes of the maxStackHeight array will be changed
				// as the loop progresses
			 	if maxStackHeight[i] < maxStackHeight[j] + allBoxes[i].h:
				 	maxStackHeight[i] = maxStackhieght[j] + allBoxes[i].h;

	// set maxStackOfBoxes to a negative value for comparisons
	int maxStackOfBoxes = -1;

	// search the maxStackHeight array for the maximum value
	for (i=0 to n-1):
		maxStackOfBoxes = max(maxStackOfBoxes, maxStackHeight[i]);
		
	return maxStackOfBoxes;
```

This method includes one nested for loop, which means that the time complexity will be **O(n^2)**.

# Example


