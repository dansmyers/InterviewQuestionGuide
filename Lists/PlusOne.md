# Problem
Given an array of integer representing a non-negative integer and each element in the array represents a single digit, add/plus one to the integer representation and return the new integer. 

# Example
1. Input: [4, 2, 5]   ; Output: [4, 2, 6]
The array integer representation 425 becomes 426 when you add one. 
2. Input: [3, 6, 3, 9]   ;  Output: [3, 6, 4, 0]
The array integer representation 3639 becomes 3640 when you add one. 

# Mid-point Check
1. What would the array input of [3, 9, 9] return with the function plusOne(array)? 
2. What would the array input of [9, 9] return with the function plusOne(array)?
3. What would the array input of [ ] return with the function plusOne(array)? This is an empty array. 

# Solution
Things to think about
*how to implement when the digit is a 9 
*how to add another digit when needed 

Steps 
1. Instigate a function that takes an input of an array of integers named plusOne. 
2. Declare an array list to keep track of the ending sum to return. 
3. If the inputted array is empty or null, then return with an array with a digit of 1. 
4. Declare a carry integer in case the inputted array needs to 
4. Instigate a for loop to start from the last digit of the array to the first digit of the array. Go through the for loop one by one backwards. If a digit in the array is 9, then change that digit to 0 and continue on looping. If it is any other digit (0-8), then add to that digit the carry integer and break the for loop. 
5. Return the updated array. 

**Example 1:** 
Input: array integer of 365 
1. Not an empty or null array, so follow through the code. 
2. The last digit (5) is not 9, so add 5 + 1 to it so it will be 6. Break the for loop cause no other operations are needed.
3. Only 1 change was done (only the 5 was updated to 6), and then directly return the updated array to be 366. 
Output: array integer of 366

**Example 2:**
Input: array integer of 89
1. Not an empty or null array, so follow through the code. 
2. The last digit (9) is 9, so change that digit to 0. 
3. Continue looping through. The next digit (8) is not 9, so change to 9 because you add 8 and carry's value of 1. Break the for loop. 
4. Return the updated value as 90. 

# Complexity Analysis
**O(n)**

# Code Implementation
```
public void plusOne(int[] array) { 
    if (array == null || array.length == 0) {
         int[] one = {1};
         return one;
    }
    int carry=1;
    for(int i= array.length-1;i>=0;i--){
        if(array[i]==9){
          array[i]=0;
        }
        else{
           carry = carry + digits[i];
           array[i]= carry;
           break;
        }
    }
    return array;
} 
```
  
# Review Questions
1. How would the code implementation be different if it was not a given that the array with non-negative? 
2. How does the code implementation handle if the array needs to grow where a new digit needs to be added? 
