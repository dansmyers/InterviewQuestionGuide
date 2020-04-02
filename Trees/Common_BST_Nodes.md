# Question
Given two binary search trees, find an efficient way to print the nodes shared by both trees. You may use auxiliary data structures.  

*Challenge:* What is the **time complexity** of your solution?

Before beginning, remember the **features of a binary search tree** (BST):
- BSTs maintain *order*. In other words, all the **nodes are sorted**.
- A parent can have **no more than two** children.
- All of the children to the **right** of a parent hold a value *less than* that of the parent.
- All of the children to the **left** of a parent hold a value *greater than* that of the parent.


## Solution #1 (Not so good.)
**In the second tree, search for every node of the first tree.**

*Time Complexity:*  
O(# of nodes in the first tree * height of the second tree)

## Solution #2 (A little better.)
**Use two arrays.**  

Create two `arrays`, one for the nodes of the first tree ("`tree1`"), and one for the nodes of the second tree ("`tree2`").  

Traverse `tree1`, and as you do so, save the value of each node by storing them in an array.  
(Make sure that the values remain sorted!)

Then, do the same thing for `tree2`.

After you have an array of values for each tree, find the **intersection** of the two arrays.  

*Time Complexity:*  
O(# of nodes in the first tree * # of nodes in the second tree)

## Solution #3 (Best, most efficient.)
**Use two stacks.**

You might be used to traversing trees by way of **recursion**. But for this solution to work, we'll need to traverse the trees by way of **iterative inorder traversal**. We'll need two `stacks` to do that.  

For this solution, it's easier to explain with pseudocode.

We'll assume that a node has the following attributes:  
- `x.key` is the node's value
- `x.left` points to the node's left child
- `x.right` points to the node's right child 

```

// you'll need a function for performing inorder traversals
inorder(root) {
    if (root != NULL) {
        inorder(root.left)
        print(root.key)
        inorder(root.right)
    }
}

// and here's the function that prints the common nodes
print_common_nodes(root1, root2) {  // pass in the roots of each tree
    
    // we need two stacks
    stack1 = new Stack()
    stack2 = new Stack()
    
    // a loop!
    while (true) {
        
        // push the trees onto their respective stacks
        if (root1 != NULL) { // tree1
            stack1.push(root11)
            root1 = root1.left
        }
        
        else if (root2 != NULL) { //  tree2
            stack2.push(root2)
            root2 = root2.left
        }
        
        // if both of the roots are NULL
        else if (root1 == NULL and root2 == NULL) {
            // check the stacks
            root1 = s1.peek()
            root2 = s2.peek()
            
            // and if the keys are the same...
            if (root1.key == root2.key) {
                // remove from the stack and print!
                // (only print one key because they match)
                print(root1.key)
                s1.pop()
                s2.pop()
                
                // continue with the inorder traversal
                root1 = root1.right
                root2 = root2.right
                
            }
            
            // if the keys are NOT the same...
            else if (root1.key < root2.key) {
                s1.pop()
                root1 = root1.right
                root2 = NULL
            }
            
            else if (root1.key > root2.key) {
                s2.pop()
                root2 = root2.right
                root1 = NULL
            }
        }
        
        // if you reach this point, both roots and stacks are empty
        else break
        
    }
}
```


###### Sources: https://www.geeksforgeeks.org/print-common-nodes-in-two-binary-search-trees/

###### Sources: https://gist.github.com/dilipkondaparthi/4f4f7b49e1f6d507d71305bdc8764f02

###### Sources: https://www.geeksforgeeks.org/union-and-intersection-of-two-sorted-arrays-2/
