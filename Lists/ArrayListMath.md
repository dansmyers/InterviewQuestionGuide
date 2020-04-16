# The Challenge
In this interview challenge question, given an unsorted ArrayList of numbers, solve for the following and print them to the console:
1. Mean
2. Median
3. Range

# Example Problem
#### A program is set up such that it prompts a user to input double values into an ArrayList. Given that the user inputted the values {3.0, 4.2, -5.1, 11.2, 0.0, 1.01}, _calculate the **mean, median, and range** of the contents of the ArrayList_. 


To solve such a problem, one must be familiar with the mathematical formulas for mean, median, and range:
* The **mean** is the _average_ value of the elements in the set, or the sum of all elements divided by the number of elements.
* The **median** is the _middle_ element in the set when arranged in ascending or descending order. If the set has an even number of elements, then the median is the _mean_ of the two middle elements. 
* The **range** is the difference between the largest and smallest elements of the set.


## Solving

The first step to solving this problem by hand would be to rearrange the set of elements, or the ArrayList, into ascending order, giving us {-5.1, 0.0, 1.01, 3.0, 4.2, 11.2}. This can be accomplished with the `Collections.sort(exampleArrayList);` method of the Collections class. You must `import java.util.Collections;` before you can use the method.

**_You must sort the set/ArrayList before solving for the median and range._**

Then, we would add up the total number of elements in the set, which would be 6. This can be accomplished with the `exampleArrayList.size()` method. 

With this baseline of information, we can begin to solve the three problems of mean, median and range.


### Mean

To calculate mean, we must take the sum of all elements in the set, 14.31, then divide that value by the number of elements in the set, 6. This gives us a mean of 2.385. 
```java
double sumOfElements = 0;
for (int n = 0; n < exampleArrayList.size(); n++) {
  sumOfElements += exampleArrayList.get(n);
}

System.out.println("The mean is ");
System.out.printf("%.5f", (sumOfElements / exampleArrayList.size()));
```


### Median

To calculate median, we must first solve for n, which will be the total number of elements in the set divided by two, which would give us 3 in our example. If the number of elements in the set is odd, the (n + 0.5)th element in the set is the median. If the number of elements in the set is even, which our example is, then we would find the mean of the nth and n + 1th elements in the set, which would be the mean of the third and fourth elements of the set, 1.01 and 3, giving us a median of 2.005.
```java
if (exampleArrayList.size() % 2 == 0) {
    int halfEven = (exampleArrayList.size() / 2);
    System.out.print("The median is ");
    System.out.printf("%.5f", ((exampleArrayList.get(halfEven - 1) + exampleArrayList.get(halfEven)) / 2));
}
else {
    double halfOdd = (exampleArrayList.size() / 2);
    int index = (int) (halfOdd - 0.5);
    System.out.println("The median is " + (exampleArrayList.get(index)));
}
```


### Range

To calculate range, we subtract the first element of the set from the last element of the set. In our example, this would be 11.2 and -5.1, giving us 16.3. 
```java
System.out.println("The range is " + ((exampleArrayList.get(exampleArrayList.size() - 1) - exampleArrayList.get(0))));
```


## Complexity Analysis
Since this challenge is essentially asking three similar questions at once, each question can be separately analyzed for complexity:
* Sorting the ArrayList via the `Collections.sort()` method is crucial for solving the problem. This method has a complexity of **O(nlog(n))** because it utilizes a "stable, adaptive, iterative mergesort that requires far fewer than n lg(n) comparisons when the input array is partially sorted, while offering the performance of a traditional mergesort when the input array is randomly ordered. If the input array is nearly sorted, the implementation requires approximately n comparisons." [Source](https://docs.oracle.com/javase/7/docs/api/java/util/Collections.html#method_detail "docs.oracle.com Class Collections")

* Calculating the **mean** would have a complexity of **O(n)** because the calculation for mean involves going through the entire set and finding the sum, and the complexity will scale linearly with the size of the set. 
* Calculating the **median** would have a complexity of **O(n)** because the calculation for median scales linearly with the size of the set.
* Calculating the **range** would have a complexity of **O(1)** because the process will always take the same amount of time. Since all that is being done is subtracting the first element of the ArrayList from the last, this process isn't affected by the size of the ArrayList *because the ArrayList is **already sorted.***


## Final Review Questions
* How does one calculate mean, median and range (by hand)?
* What must be done before calculating median and range?
* What Java class must be imported to simplify the process in the previous question?
