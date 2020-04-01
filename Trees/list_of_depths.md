# List of Depths

## Group Members

Parker Smith, Jessica Salvino, Cameron DeLone, Robin Loh

## Problem

Given a binary tree, design an algorithm which creates a linked list of all the
nodes at each depth. For example, if you have a tree with depth X, then you'll
have X linked lists.

***Input:*** a binary tree

***Output:*** X linked lists if the height of the tree is X. Each linked list
will have all the nodes of each level

### Example

Before attempting to solve this problem, lets look at an example BST and
determine what the output should be if it was the input in our algorithm.

Below is our example BST:

```
                        1
                        |
                  -------------
                  |            |
                  2            3
                  |            |
              ---------    ---------    
              |       |    |       |
              4       5    6       7
```

Based off of our example BST, we can determine that the height is 3. Since the
height is 3 we know that our output should consist of 3 linked list.

Now that we know how many linked lists we will have, lets determine what the
linked lists should consist of.

For this problem we want to create a linked list of all the nodes at each depth.
So with that being established, our first depth is depth 0, which is 1. Our next
depth is depth 1, which consists of the nodes 2 and 3. Our final depth is depth
2, which consists of the nodes 4, 5, 6, and 7.

So based off our findings above, the solution will be:

```
List 1: ->1
List 2: ->2->3
List 3: ->4->5->6->7
```

Now lets implement a solution to solve this problem.

## Solution

In order to solve this problem, we can traverse the BST any way we want as long
as we know which level we're on as we do so.

In this case, we will implement a pre-order traversal algorithm, where we pass
level + 1 the next recursive call. The code below implements this solution
using depth-first search.

        void createLevelLinkedList(TreeNode root, ArrayList<LinkedList<TreeNode>> lists, int level) {
          if (root == null) return; // base case

          LinkedList<TreeNode> list = null;
          if (lists.size() == level) { // Level not contained in list
              list = new LinkedList<TreeNode()>;
              // levels are always traversed in order
              // if this is the first time we've visited level i
              // then we must have seen levels 0 through i - 1
              // thus we can add the level at the end
              lists.add(list);
          } else {
            list = lists.get(level);
          }

          list.add(root);
          createLevelLinkedList(root.left, lists, level + 1);
          createLevelLinkedList(root.right, lists, level + 1);
        }

        ArrayList<LinkedList<TreeNode>> createLevelLinkedList(TreeNode root) {
          ArrayList<LinkedList<TreeNode>> lists = new ArrayList<LinkedList<TreeNode>>();
          createLevelLinkedList(root, lists, 0);
          return lists;
        }

The above implementation utilizes pre-order traversal and depth-first searching.
Meaning the algorithm will visit the current node before its child node and will
always start at the root.

Similar to our example above, this implementation will solve the problem in a
similar manner by starting at depth 0. Our solution will utilize a variable
called level in order to keep track of the depth we are at. The variable level
will always start at 0, or the root.

In order to solve the problem, we are using recursive calls to create linked
lists at each depth starting with the root. In this case, the algorithm will
check if the node is null, if so it will return, if not it will continue. At
depth 0 our node is 1 so we will continue. Continuing through we will create a
linked list called list, then use the get() method to call the element at
index level, which is 0 and the element at index 0 is 1, then add the element
to the linked list. Then the algorithm will recursively call itself to traverse
the tree from the left and then the right, creating linked lists at each level.

Thus, are first linked list consists of the element 1.

Using the recursive call, we create linked lists at each depth exactly the same
way. So at level 1, we will use the same method to create a linked lists that
will consist of 2 and 3. Then we will continue the recursive calls to create a
linked list at level 2 which will consist of 4, 5, 6, and 7. Finally, we will
meet our base case then return all of our linked lists, thus solving the
problem.

This solution runs in O(N) time.
