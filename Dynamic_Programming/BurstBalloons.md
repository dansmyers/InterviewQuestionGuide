# Burst Balloons

![alt text](https://github.com/SALVINOJ/InterviewQuestionGuide/blob/master/Dynamic_Programming/BurstBalloonsMeme.png "Meme by Jessica Salvino") 

## Problem

You are given an array of N balloons. Each balloon has a certain value of coins associated with it. The goal of this problem is to burst the balloons in an order that maximizes the possible profit earned. When you burst balloon i, the number of coins earned is the balloon's value to the left * the burst balloon's value * the balloon's value to the right. Let this be written as B[i-1] * B[i] * B[i+1]. If there is no balloon adjacent to the popped balloon (either left or right) allow that value to equal 1, assuming an extra 1 at each boundary. 

Try an example: For B[ ] = {5, 6} what is the maximum possible profit earned?

    There are two possible outcomes, but which yields the maximum number of coins?
    
    1.  First burst = 6,  Coins = 5 * 6 * 1
        Second burst = 5, Coins+= 1 * 5 * 1
        Total = 35
    
    2.  First burst = 5,  Coins = 1 * 5 * 6
        Second burst = 6, Coins+= 1 * 6 * 1
        Total = 36
        
    The second outcome gives you the maximum value being 36 coins. 
    
 ## Visual Example
 
 You are given an array of 4 balloons, B[1, 2, 3, 4]. Try and find the maximum possible profit when popping the balloons
 (this example does not show the maximum possible profit).
 
 ![alt text](https://github.com/SALVINOJ/InterviewQuestionGuide/blob/master/Dynamic_Programming/Burst%20Balloons%20Example.png "Example by Jessica Salvino") 
    
**Check-in:** Solve the following example by hand: B[ ] = {3, 1, 5, 8}.

## Solution 

The Burst Balloon problem can be solved by **recursion**, however there is a more optimal and efficient solution that can be solved through **dynamic programming** . We are going to use bottom up dynamic programming to solve this question. The idea is to get every subarray of every length of this array and for every subarray find the last balloon which needs to burst in order to maximize the value for that subarray. Once you have calculated that for every subarray, you can use that data to find the maximum value you can get from the array. 

Take a 2D array and make the number of columns and the number of rows equal to the size of the original array. 
In this case you will have 4 columns and 4 rows:
       
|     | 0   | 1   |  2  |  3  |
| --- |:---:|:---:|:---:|:---:|
|  0  |     |     |     |     |
|  1  |     |     |     |     |
|  2  |     |     |     |     |
|  3  |     |     |     |     |

Every square in this matrix is capable of holding two values. The first being the maximum value you can get from a subarray and the second being the last balloon in the subarray. We will start with the smallest subarray we can, where length = 1, and look at every subarray where length = 1. 

The first subarray starts at 0 and ends at 0, so the balloon popped would be of value 3 and the last balloon popped would be at index 0. This allows the first square to be completed by 3,0. 
Take a moment to fill in the rest of the matrix.

The rest of the matrix looks like this: 

|     | 0   | 1   |  2  |  3  |
| --- |:---:|:---:|:---:|:---:|
|  0  | 3,0 | 30,0|159,0|167,3|
|  1  |     | 15,1|135,2|159,3|
|  2  |     |     | 40,2| 48,3|
|  3  |     |     |     | 40,3|

The top right corner of the matrix is your answer. The maximum profit earned from popping 4 balloons of values 3, 1, 5, and 8 is 167 coins with balloon at index 3 being the last balloon to burst. However, how do we find the order in which the balloons were burst? To find the order, we must backtrack through the matrix. To do this, you must look at the highest value in the subarray that is left and look at which index that balloon is located. 

This will leave you with the solution being 1, 5, 3, 8 with a max value of 167 coins. 

To outline this, we would first, consider a sub-array from indices left to right(inclusive).
If we assume the balloon at index last to be the last balloon to be burst in this subarray, we would say the coins gained would be - B[left-1] * B[burst] * B[right+1]

Also, the total coins gained would be this value, plus dp[left][last – 1] + dp[last + 1][right], where dp[i][j] means maximum coin gained for sub-array with indices i, j.
Therefore, for each value of Left and Right, we need find and choose a value of Last with maximum coin gained, and update the dp array.

The Answer is the value at dp[1][N].

Now that we have outlined the solution, lets encode it in Python. 


```Python
#Burst Balloons
def getMax(B): 
    N = len(B) 
    B = [1] + B + [1]# add neighboring balloons 
    dp = [[0 for x in range(N + 2)] for y in range(N + 2)]# Declare DP Array 
      
    for length in range(1, N + 1): 
        for left in range(1, N-length + 2): 
            right = left + length -1
  
            # For a sub-array from indices left, right 
            # This innermost loop finds the last balloon burst 
            for last in range(left, right + 1): 
                dp[left][right] = max(dp[left][right], \ 
                                      dp[left][last-1] + \ 
                                      B[left-1]*B[last]*B[right + 1] + \ 
                                      dp[last + 1][right]) 
    return(dp[1][N])
    

B = [3, 1, 5, 8] 
print(getMax(B)) 
       
```
  
## Review
How could you solve this problem recursively? After implementing dynamic programming, how is it more efficient than recursively solving the problem? What overlaps do you see when attempting to recurvsively solve Burst Ballons AFTER solving it via dynamic programming?
