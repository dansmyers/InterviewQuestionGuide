# Convert Binary Tree to its Mirror
Description: 
Given a binary tree, write an algorithm to invert the tree.

## The Problem: 
You may ask yourself when and how would inverting a binary tree be useful. As a newbie I asked myself that same question. The answer is, it is useful in showing how you breakdown a problem and how well you understand data structures. If you are like me and like to see practical examples to help you learn, well you are out of luck. A quick google search "practical applications of mirroring binary trees” just returned the controversy of this question being asked in interviews. Take a look at the links below for a fun read of the perception of this particular problem.

[Hackerrank's take on Tree questions](https://blog.hackerrank.com/the-unhealthy-obsession-with-tree-questions/)

[Famous Tweet](https://twitter.com/mxcl/status/608682016205344768)

[Why do they ask this question in interviews](https://thecodebarbarian.com/i-dont-want-to-hire-you-if-you-cant-reverse-a-binary-tree)

### The good news: 
The process of Mirroring a binary tree is pretty straight forward to understand.

## Problem Description: Invert a binary Tree
An inverted binary tree also called the mirror of an input tree is another binary tree with left and right childern swaped resulting in a mirror image of the input tree.

## Example:
Starting Tree T

![Image Inverted BT](https://raw.githubusercontent.com/mariellaPariente/InterviewQuestionGuide/master/Trees/inverted%20BT.png)

Resulting Tree after mirroring M(T)

![Image Input BT](https://raw.githubusercontent.com/mariellaPariente/InterviewQuestionGuide/master/Trees/Input%20tree%20BT.png)


## The Solution:
    Perform an inorder traversal and swap the children and recursively solve the smaller sub-problems of the left and the right sub-tree
    
    There are three steps that are executed for every node of the BT
    1. If the tree is empty return NULL
    2. Call the mirror function for the left-subtree or the right-subtree
    3. For every node swap its left and right child 

## Pseudocode:
     void mirror (struct node* node) {
	// base case: if tree is empty
	if (node == NULL)
		return;
	
	else
	{
		struct node* temp;

		mirror(node->left);
		mirror(node->right);

 		// swap left subtree with right subtree
		temp = node->left;
		node->left = node->right;
		node->right = temp;
	}

}
## Walking Through the Tree visually:
![Image Input BT](https://raw.githubusercontent.com/mariellaPariente/InterviewQuestionGuide/master/Trees/Input%20tree%20BT.png) 
   
## Concept Review:
