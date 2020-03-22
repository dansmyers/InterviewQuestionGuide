# Dutch National Flag

## Problem

![Image of the Dutch national flag](https://github.com/ewurst/InterviewQuestionGuide/blob/master/Recursion_and_Divide-and-Conquer/Dutch%20National%20Flag.jpg)

Based on the design of the Dutch national flag, as depicted above, which consists of three horizontal strips: red, white, and blue. Initially, think of having an assortment of balls in these three colors – the exact number is immaterial. The goal is to organize these balls into groups based on color, and then order the groups to match the flag.Now, apply the same concept to three different numbers, given in any order, and sort into ascending order.

```
Given {2, 4, 2, 3, 4, 2, 3, 2, 4, 4, 2, 3}, sort into {2, 2, 2, 2, 2, 3, 3, 3, 4, 4, 4, 4}

Given {5, 1, 7, 7, 1, 5, 5, 1, 7, 1}, sort into {1, 1, 1, 1, 5, 5, 5, 7, 7, 7}
```

The process is the same regardless of what the three numbers areand how many of each there is.

**Check-in:** Given {3, 9, 9, 12, 3, 12, 12, 12, 9, 3, 9}, what should you return?

## Solution

When coding the solution, it is best to turn towards **quicksort**, as the Dutch national flag problem is essentially a three-way quicksort. In traditional quicksort, an array of numbers is split into two parts based on a **pivot** – numbers less than and equal to the pivot, and numbers greater than the pivot. With the Dutch national flag problem, you end up with three segments:

1. Set of the number less than pivot
2. Set of pivot number
3. Set of the number greater than pivot

However, this listing is dependent on the pivot being the middle of the three values, and, depending on how you build your program, you will most likely not be able to guarantee the pivot being the middle value. Since we will be using the last number in the array as our pivot, we will use an additional method called *partition* to help us separate our array into these three parts regardless ofthe pivot’s value.

### Quicksort 

Since we will be using the helper method *partition*, our *quicksort* method with consist only of our first base case, the call to *partition*, and recursive calls with *partition*’s results. Our first base case is to check if the given array has one or zero elements, in which case the array is already in order. Additionally, there is a for loop to see if an array of a longer length is already sorted – this exists to cut down unnecessary recursive calls of sorted numbers.

```Java
static int i = 0;
static int j = 0;

public static void quicksort(int [] arr, int low, int high) {
    if(low >= high) {
        return;
    }
  
    boolean isSorted = true;
    for(int i = 0; i < arr.length; i++) {
        if(i != arr.length-1) {
            if(arr[i] > arr[i+1]) {
                isSorted = false;
            }
        }
    } 
  
    if(!isSorted) {
        partition(arr, low, high);
        quicksort(arr, low, i);
        quicksort(arr, j, high);
    } else {
        return;
    }
}
```
#### i & j

The integers **i** and **j** seen above *quicksort* are two global variables that we will see more if in our *partition* method. For now, know that **i** and **j** exist as variables that hold the indices enclosing the sorted part of the array. This ensures the recursive *quicksort* calls focus on smaller, unsorted chunks of the array.

### Partition

From *quicksort*, we move to the *partition* method – this is where the array will be split into smaller parts and where those parts will be sorted. The method starts with our second base case – having two elements. If there are two elements, check their order and adjust accordingly. Then our global integers i and j will be set to the indices these values sit at 
so they will not be resorted when returning to *quicksort*. 

If the base case is not met, then two new integers are introduced – mid, which holds the current index being examined, and piv, or pivot, which we have made the last value in the given array. While there is another index for mid to be compared against, we check to see if the value at the mid index is less than, equal to, or greater than the pivot value, swapping values and incrementing indices accordingly.

At the end of the method i gets the index of one less than the starting index of the given array, and j gets the index held in mid, which, after the while loop, is equal to one index higher than the last index of the given array. Therefore, upon returning to *quicksort*, the part just sorted within the while loop is excluded from the recursive calls.

```Java
public static void partition(int [] arr, int low, int high) {
    if(high-low <= 1) {
        if(arr[high] < arr[low]) {
            int temp = arr[high];
            arr[high] = arr[low];
            arr[low] = temp;
        }
        i = low;
        j = high;
        return;
    }
    int mid = low;
    int piv = arr[high];
    while(mid <= high) {
        if(arr[mid] < piv) {
            int temp = arr[low];
            arr[low] = arr[mid];
            arr[mid] = temp;
            low++;
            mid++;
        } else if(arr[mid] == piv) {
            mid++;
        } else if(arr[mid] > piv) {
            int temp = arr[mid];
            arr[mid] = arr[high];
            arr[high] = temp;
            high--;
        }
    }
    i = low-1;
    j = mid;
}
```
### Main

Finally, in our main method, we instantiate our array, call *quicksort*, and then print out the now sorted array.

```Java
public static void main(String [] args) {
    int[] a = {2, 4, 2, 3, 4, 2, 3, 2, 4, 4};
    quicksort(a, 0, a.length-1);
    
    for(int i = 0; i < a.length; i++) {
        System.out.println(a[i] + (i == a.length-1 ? "" : ", "));
    }
}
```


## Review
