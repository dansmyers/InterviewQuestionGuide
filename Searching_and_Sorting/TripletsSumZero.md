# Problem
When given an array of distinct N integers, return all triplet sets that sum up to 0 such that a + b + c = 0 by creating a function: findTriplets(). If no triplet sets exist, then print out "no triplet sets found". 

# Example
Given array = [-4, -2, 0, 2, 4], 
The function findTriplets() will return the unique triplet sets of: 
[
  [-4, 0, 4],
  [-2, 0, 2], 
]

# Mid-point Check
1. Given array = [-5, -4, 2, 6, 9], what would the function findTriplets() return? 
2. Given array = [0, 1, 2, 3, 4], what would the function findTriplets() return? 

# Solution
1. Write out a function with an input of an integer array. 
2. Make an integer variable to keep track of the inputted array's length. 
3. Make a boolean to keep track if a triplet sum gets returned. 
4. Implement 3 nested for loops to check one by one if triplet sets exist to sum to zero. If a triplet set is found, print out the triplet set's elements. Change the boolean element to true which means that a triplet sum has been found. 
5. After iterating through all 3 loops, check if the boolean element is true or false. If the boolean element is false, then the array set does not contain a triplet set and return an appropriate message to the user. 

**Example:** 
int array[] = {-5, -1, 0, 1, 5}; 
findTriplets(array); 

Iterating through all combinations to find the triplet sets with 3 for loops will be as follows:
1. -5, -1, 0 
2. -5, -1, 1
3. -5, -1, 5
4. -5, 0, 1 
5. -5, 0, 5    ... returns with a sum of 0 so return this triplet set 
6. -5, 1, 5
7. -1, 0, 1  ... returns with a sum of 0 so return this triplet set
8. -1, 0, 5
9. -1, 1, 5
10. 0, 1, 5

Output: 
-5, 0, 5
-1, 0, 1

# Complexity Analysis
**O(n^3)**
1. In the outer loop, you would have to examine n elements. In the middle loop, you would have to examine n-1 elements. In the inner loop, you would have to examine n-2 elements. The upper bound is the array's length, n. 
2. Each iteration you go into, you would have to examine 1 fewer elements. You will have to loop through all combinations of elements to ensure that all triplet sets are found, which is n to the power of 3 because there are 3 nested for loops. 

# Code Implementation
```
public void findTriplets(int[] array) { 
    int length = array.length; 
    boolean exists = true; 
    for (int outer = 0; outer < length - 2; outer++) { 
        for (int middle = outer + 1; middle < outer -1; middle++) { 
            for (int inner = middle +1; inner < middle ; inner++) { 
                if (array[outer]+array[middle]+ array[inner] == 0){ 
                    System.out.print(array[outer] + " " + array[middle] + " " + array[inner] + "\n"); 
                    exists = true; 
                } 
            } 
        } 
    } 
    if (exists == false){
        System.out.println("no triplet sets found"); 
    }
} 
```
  
# Review Questions
1. What is this kind of searching method called? 
2. How would this implementation work better if we sorted the array list first? 

