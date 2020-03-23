# Diagonal Sum of a Binary Tree

## Problem

Consider lines of slope -1 passing through the nodes in the given binary tree. Assume that the child of any given node makes a 45 degree angle with the parent. Print the diagonal sums of the elements belonging to the same line in a binary tree.

![Image of a binary tree with lines of slope -1 passing through the nodes](https://github.com/ewurst/InterviewQuestionGuide/blob/master/Trees/Diagonal%20Sum%20of%20a%20Binary%20Tree%20Write-up%20set%20up%20example.png)

Given the binary tree above, by examining where the lines of slope -1 are, we're able to determine which values go into which summation. We will elaborate on the vd labels later, which have to do with the vertical distances of each node.

```
The first summation, which corresponds to a vertical distance of 0, would be: 20 + 30 + 35 + 40 = 125
The second summation, which correponds to a vertical distance of 1, would be: 10 + 15 + 18 + 25 + 28 + 32 + 34 = 162
The third summation, which corresponds to a vertical distance of 2, would be: 5 + 8 + 12 + 22 + 26 + 27 = 100
```

**Check-in:** Given the binary tree below, calculate the diagonal summations of the elements belonging to the same line.

![Image of a binary tree with lines of slope -1 passing through the nodes](https://github.com/ewurst/InterviewQuestionGuide/blob/master/Trees/Diagonal%20Sum%20of%20a%20Binary%20Tree%20Write-up%20example%201st.png)

## Solution

The Diagonal Sum of a Binary Tree problem uses **diagonal traversal** in order to visit each node and calculate the diagonal sum. In order to diagonally traverse through a binary tree, we need to keep track of which nodes belong to the same diagonal line. We can do this by finding the **vertical distances** of each node from the root. Nodes that are on the same diagonal line as the root node have a vertical distance of 0. Nodes that are on the diagonal line directly below the diagonal line with a vertical distance of 0 have a vertical distance of 1. The next diagonal line proceeding down would have a vertical distance of 2 and so on and so forth.

![Image of a binary tree with lines of slope -1 passing through the nodes](https://github.com/ewurst/InterviewQuestionGuide/blob/master/Trees/Diagonal%20Sum%20of%20a%20Binary%20Tree%20Write-up%20example%202nd.png)

From here, we can determine the diagonal sum by adding the values of each node that are on the same diagonal line.

Now, how would we solve this problem algorithmically?

The basic algorithm for this problem can be summed up in five steps:

1. Take the root node as the current node and assign it a vertical distance 0.
2. Find the right child of the current node and assign it the current node’s vertical distance. Store the node and its      vertical distance.
3. Find the left child of the current node and assign it the current node’s vertical distance plus one. Store the node and its vertical distance.
4. Repeat Steps 2, 3, & 4 recursively for each node until there are no more nodes to process.
5. Calculate the sum of the values that correspond to a node with the same vertical distance.


## Example

In order to prove that the above Python implementation holds, we will insert the binary tree into the implementation in order to calculate the diagonal sum.

![Image of a binary tree with lines of slope -1 passing through the nodes](https://github.com/ewurst/InterviewQuestionGuide/blob/master/Trees/Diagonal%20Sum%20of%20a%20Binary%20Tree%20Write-up%20illustrated%20example%20solution.png)

```Python
if __name__ == '__main__': 
    # creates a tree to sum
    root = newNode(1)  
    root.left = newNode(10)  
    root.right = newNode(5)  
    root.right.left = newNode(2)
    root.right.right = newNode(8)
    root.right.right.right = newNode(17)
    root.left.left = newNode(9)
    root.left.right = newNode(12)
    root.left.right.left = newNode(11)
    root.left.right.left.right = newNode(7)

    # calls function to sum created tree  
    diagonalSum(root) 
```



## Review

After exploring the usefulness of a diagonal traversal in order to calculate the diagonal sum of a binary tree, are there any other binary tree traversals that could be used in this manner and how would they be used? 
