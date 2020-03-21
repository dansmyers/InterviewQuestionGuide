# Coin Change 

## Problem

Given a value N, if we want to make change for N cents, and we have infinite supply of each of S = { S<sub>1</sub>, S<sub>2</sub>, ..., S<sub>m</sub>} valued coins, how many ways can we make the change? The order of coins doesn’t matter.

    For N = 4 and S = { 1, 2, 3 }, there are four solutions:
    { 1, 1, 1, 1 }, { 1, 1, 2}, { 2, 2 }, and { 1, 3 }
    Therefore, output should be 4.

    For N = 10 and S = { 2, 5, 3, 6 }, there are five solutions:
    { 2, 2, 2, 2, 2 }, { 2, 2, 3, 3 }, { 2, 2, 6 }, { 2, 3, 5 }, and { 5, 5 }
    Therefore, the output should be 5.

**Check-in:** Solve the following example by hand: N = 9, S = { 9, 4, 1 }.



## Solution

The Coin Change problem exhibits **overlapping subproblems**, meaning that it recursively visits the same subproblemover and over again. Because of this characteristic, we can solve the problem through **dynamic programming** by performing the following steps:

1. Characterizing the structure of an optimal solution,
2. Recursively defining the value of an optimal solution, and
3. Computing the value of an optimal solution

The first step is to **characterize the optimal substructure**. To count the total number of solutions, we can divide all solutions into two sets: (a) Those that do not contain the coin S<sub>m</sub> and (b) Those that contain at least one S<sub>m</sub> coin. With this substructure in mind, we can now **recursively define the value of an optimal solution**. If change(N, M, S[] ) is the function to count the number of solutions, it can be written as the sum of change(N, M-1, S[]) and change(N-S<sub>m</sub>, M, S[] ). 

To **compute the value of an optimal solution**, we must also consider the **base cases**. There is only one way to make change for 0 cents, therefore if N is equal to 0, the algorithm should return 1. There’s no way to make change for less than 0 cents, or with 0 or less coins. Therefore, in these cases, the algorithm should return 0. If none of these base cases apply, the subproblem will be solved according to our recursively defined value of an optimal solution described previously.

Now that we’ve outlined our solution, we can encode it in Java:

```
public static int change(int N, int M, int S[]) {
    if(N == 0)
        return 1; 
        
    if(N < 0 || (N >= 1 && M <= 0))
        return 0;
        
    return change(N, M-1, S, lookup) + change(N-S[M-1], M, S, lookup);
}
```

While the above algorithm works, it contains overlapping subproblems that it solves repeatedly. For this reason, our recursive solution is incredibly slow, running in exponential time. Instead of solving the same subproblems again and again, we should take advantage of the overlap by solving each subproblem once and storing the solution to be looked up in constant time. This can be accomplished through **memoization**. We will “memoize” the inefficient algorithm by maintaining a table with subproblem 
solutions. Each time the algorithm encounters a subproblem, it will check if the subproblem’s solution is already in the table. If it’s not there, it will solve the subproblem recursively and include it in the table. The solution will then be retrieved from the table and returned by the algorithm. 

We can memoize our algorithm by storing and retrieving solutions using Java’s HashMap:

```
public static int change(int N, int M, int S[], Map<String, Integer> lookup) {
    if(N == 0)
        return 1;
        
    if(N < 0 || (N >= 1 && M <= 0))
        return 0;

    String key = N + “|” + M;
    
    if(!lookup.containsKey(key)) {
        lookup.put(key, change(N, M-1, S, lookup) + change(N-S[M-1], M, S, lookup);
    }
    
    return lookup.get(key);
}
```

We can now test our algorithm in main by calling the change() method with our example values: 

```
public static void main(String[] args) {

    Map<String, Integer> lookup1 = new HashMap<>();
    int n1 = 4;
    int s1[] = {1, 2, 3}; 
    int m1 = s1.length; 
    System.out.println(makeChange(n1, m1, s1, lookup1));
    
    Map<String, Integer> lookup2 = new HashMap<>();
    int n2 = 10;
    int s2[] = {2, 5, 3, 6};
    int m2 = s2.length;
    System.out.println(makeChange(n2, m2, s2, lookup2)); 
}
```

To illustrate the solution method, we can apply our recursive, dynamic programming algorithm to the example N = 4 and S = { 1, 2, 3 }. Please note that indentation is used to demonstrate where recursive calls are being made, and the following key is helpful in identifying how values are being returned. 

```html
<div class="text-purple"> Red </div> indicates a return of 1 from the first base case N == 0. 



```
