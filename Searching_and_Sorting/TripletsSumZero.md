# Problem
When given an array of distinct N integers, return all triplet sets that sum up to 0 such that a + b + c = 0 by creating a function: findTriplets(). If no triplet sets exist, then print out "no triplet sets found". 

# Example
Given array = [-4, -2, 0, 2, 4], the function findTriplets() will return the unique triplet sets of: 
[
  [-4, 0, 4],   since -4 + 0 + 4 = 0
  [-2, 0, 2],   since -2 + 0 + 2 = 0
]

Given array = [3, 6, 90], the function findTriplets() will return:
"no triplet sets found". 

# Mid-point Check
1. Given array = [-5, -4, 2, 6, 9], what would the function findTriplets() return? 
2. Given array = [0, 1, 2, 3, 4], what would the function findTriplets() return? 

# 3 For Loops: Solution
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
5. -5, 0, 5    ... returns with a sum of 0 so return this triplet set of [-5, 0,5]
6. -5, 1, 5
7. -1, 0, 1  ... returns with a sum of 0 so return this triplet set of [-1, 0, 1]
8. -1, 0, 5
9. -1, 1, 5
10. 0, 1, 5

Output: 
[-5, 0, 5]
[-1, 0, 1]

# 3 For Loops: Complexity Analysis
**O(n^3)**
1. In the outer loop, you would have to examine n elements. In the middle loop, you would have to examine n-1 elements. In the inner loop, you would have to examine n-2 elements. The upper bound is the array's length, n. 
2. Each iteration you go into, you would have to examine 1 fewer elements. You will have to loop through all combinations of elements to ensure that all triplet sets are found, which is n to the power of 3 because there are 3 nested for loops. 

# 3 For Loops: Code Implementation
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
3. Can you make this solution more efficient? 
   **YES! There are other solutions with a Big O notation of no more than O(n^2).**

# Sort List: 1st efficient solution
1. Implement a boolean to keep track whether or not a solution set is found. First, implement it as false. If a set is found, change it to true. At the end, if the boolean is still false, then return an appropriate statement that no triplets are found. 
2. Sort the array is ascending order from smallest to biggest using an array method. 
3. Traverse the list one by one with for loop from the first index, and ending in the last index. 
4. Implement left and right variables. The left variable will the next variable after the current variable. The right variable will be the very last integer of the array. 
5. Compare until the left variable reaches the right variable. When the program hits a triplet set that sums up to 0, then print out the match and switch the boolean to true. When the program hits a triplet set that is less than 0, then the program should increase the left variable in order to add up to a larger sum. When the program hits a triplet set that is greater than 0, then the program should decrease the right variable in order to add up to a smaller sum.

# Sort List Code Implementation 
```
public void findTriplets(int[] array) { 
    boolean exists = false; 
    Arrays.sort(arr);  //sort the array of integers into ascending order
    for (int i= 0; i < array.length; i++) { 
        int left = i + 1; 
        int right = array.length; 
        int current = array[i]; 
        while (left < right) { 
            if (current + arr[left] + arr[right] == 0){ 
                System.out.print(array[current] + " " + array[left] + " " + array[right] + "\n");
                left++; 
                right--; 
                exists = true; 
            } 
            else if (current + array[left] + array[right] < 0){
                left++; 
            }
            else{
                right--; 
            }
        } 
    } 
    if (exists == false){
       System.out.println("No triplet sets found."); 
    }
} 
```

# Sort List: complexity analysis
O(n^2): there are 2 nested loops. The first loop is to find the current starting position. The second loop is the while loop until left reaches right. By having a sorted list, the program can be more strategic in its approach on how to find a triplet set. 

# Hashing: 2nd efficient solution
**Overall concept: For every element arr[i], we find a pair with sum “-arr[i]”.**
1. Implement a boolean to keep track whether or not a solution set is found. First, implement it as false. If a set is found, change it to true. At the end, if the boolean is still false, then return an appropriate statement that no triplets are found. 
2. Traverse through the array one by one. The outer for loop (int i) will run from the first element to the 2nd to last element. The second inner for loop (int j) will run from the 2nd element to the last element of the array.
3. Create a new hash map of type Integer to store the key-value pairs.
4. Create a variable to find what integer is needed to complete the triplet set of i and j. Check if that variable is present in the hashmap or not. 
5. If the hashmap contains that element, then print the particular triplet set and change the boolean to true. If the hashmap does not contain the element, then insert the j-th element in the hashmap.
6. Continue traversing until all triplet sets are found. 

# Hashing: code implementation
```
 public void findTriplets(int array[])  { 
    boolean exists = false; 
    for (int i = 0; i < array.length - 1; i++) { 
            HashSet<Integer> map = new HashSet<Integer>(); 
            for (int j = i + 1; j < array.length; j+)  { 
                int current = -(array[i] + array[j]); 
                if (map.contains(current)){ 
                    System.out.print(array[current] + " " + array[i] + " " + array[j] + "\n");
                    exists = true; 
                }  
                else { 
                    map.add(arr[j]); 
                } 
            } 
        } 
    } 
    if (exists == false) { 
       System.out.println("No triplets sets found."); 
    } 
 } 
```

# Hashing: complexity analysis
O(n^2): there are 2 nested for loops. The outer for loop traverses through the array one by one. The inner for loop helps when you want to find what is needed to complete the sum to be 0. This is more efficient because the program is instead looking for pairs. 


