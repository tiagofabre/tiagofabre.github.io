---
layout: post
title: "Merge sort"
subtitle: "Understanding the algorithm"
comments: true
categories: "algorithms english"
---

# Definition

Designed by John von Neumann in 1945, mergesort or merge sort is a divide and conquer algorithm, that sorts collections in `O(n log n)` time and `O(n)` space complexity.

# Code

```Java
public class Main {
    
    static void merge(int[] arr, int left, int mid, int right) {
        int[] temp = new int[right - left + 1]; // left ... right + 1
        int leftIndex = left; // left ... mid
        int rightIndex = mid + 1; // mid + 1 ... right
        int tempIndex = 0; // left ... right

        // While there are elements in both slices
        // compare each pointer and store the lowest in temp
        while(leftIndex <= mid && rightIndex <= right) {
            if(arr[leftIndex] <= arr[rightIndex]) {
                temp[tempIndex++] = arr[leftIndex++];
            } else {
                temp[tempIndex++] = arr[rightIndex++];
            }
        }

        // when a pointer reaches the end of the slice
        // we just need to fill the temp array with remaining values
        while(leftIndex <= mid)
            temp[tempIndex++] = arr[leftIndex++];
        
        while(rightIndex <= right)
            temp[tempIndex++] = arr[rightIndex++];
        
        // Get the temp values and update the initial array
        for(int i=0; i < temp.length; i++)
            arr[i + left] = temp[i];
    }
    
    static void mergeSort(int[] arr, int left, int right) {
        if(left < right) {
            int mid = (left + right) / 2;
            
            mergeSort(arr, left, mid);
            mergeSort(arr, mid + 1, right);
            
            merge(arr, left, mid, right);
        }
    }
    
    static boolean isSorted(int[] array) {
        for (int i = 0; i < array.length - 1; i++) {
            if (array[i] > array[i + 1])
                return false;
        }
        return true;
    }
    
    public static void main(String args[]) {
        int arr[] = { 6, 5, 12, 10, 9, 1 };

        mergeSort(arr, 0, arr.length - 1);

        assert isSorted(arr) : "Not sorted";
        
        System.out.println("Sorted array:" + Arrays.toString(arr));
        // Sorted array:[1, 5, 6, 9, 10, 12]
  }
}
```

The algorithm recursively divides the array in the middle until it have slices of length = 1

```
fisrt round  ->   (6, 5, 12)   (10, 9, 1)     
                             ^                      
// length = 6; left = 0; right = 6; mid = ((6 + 0) / 2) -> 3

second round ->  (6)   (5, 12)   (10)   (9, 1)      
                     ^                ^             
// length = 3; left = 0; right = 3; mid = ((3 + 0) / 2) -> 1
// length = 4; left = 3; right = 6; mid = ((3 + 6) / 2) -> 4

third round  -> (6)   (5)   (12)   (10)   (9)   (1)
                          ^                   ^     
// length = 1; left = 0; right = 1; mid = ((1 + 0) / 2) -> 0; left == mid; mid + 1 == right
// length = 1; left = 3; right = 4; mid = ((3 + 4) / 2) -> 3; left == mid; mid + 1 == right
// length = 2; left = 1; right = 3; mid = ((1 + 3) / 2) -> 2
// length = 2; left = 4; right = 6; mid = ((4 + 6) / 2) -> 5

fourth round -> (6)   (5)   (12)   (10)   (9)   (1)

// length = 1; left = 1; right = 2; mid = ((1 + 2) / 2) -> 1; left == mid; mid + 1 == right
// length = 1; left = 4; right = 5; mid = ((4 + 5) / 2) -> 4; left == mid; mid + 1 == right

// length = 1; left = 2; right = 3; mid = ((2 + 3) / 2) -> 2; left == mid; mid + 1 == right
// length = 1; left = 5; right = 6; mid = ((5 + 6) / 2) -> 5; left == mid; mid + 1 == right
```

When the slices reach only one element, the algorithm calls the merge, as only one element is considered sorted.

In the merge phase, calls with more than one element will have two pointers to find the lowest elements and store them sorted in a temp array.


```java
// While there are elements in both slices
// compare each pointer and store the lowest in temp
while(leftIndex <= mid && rightIndex <= right) {
    if(arr[leftIndex] <= arr[rightIndex]) {
        temp[tempIndex++] = arr[leftIndex++];
    } else {
        temp[tempIndex++] = arr[rightIndex++];
    }
}

// when a pointer reaches the end of the slice
// we just need to fill the temp array with remaining values
while(leftIndex <= mid)
    temp[tempIndex++] = arr[leftIndex++];

while(rightIndex <= right)
    temp[tempIndex++] = arr[rightIndex++];
```

```
(6) -> (6)
(5) -> (5)
(12) -> (12)
(10) -> (10)
(9) -> (9)
(1) -> (1)

(5, 12) -> (5, 12)
(9, 1) -> (1, 9)

(6, 5, 12) -> (5, 6, 12)
(10, 1, 9) -> (1, 9, 10)

(5, 6, 12, 1, 9, 10) -> (1, 5, 6, 9, 10, 12)

```
After that the final array will receive the elements from temp


```java
// Get the temp values and update the initial array
for(int i=0; i < temp.length; i++)
    arr[i + left] = temp[i];
```
# Coplexity

## Time 

The splitting phase generates `O(log n)` levels in a recurrent tree

```
log2(8) = 3

[9, 8, 7, 6, 5, 4, 3, 2] -> n/1 = n

[9, 8, 7, 6][5, 4, 3, 2] -> n/2 + n/2 = n
[9, 8][7, 6][5, 4][3, 2] -> n/4 + n/4 + n/4 + n/4 = n
[9][8][7][6][5][4][3][2] -> n/8 + n/8 + n/8 + n/8 + n/8 + n/8 + n/8 + n/8 = n
````

The merge phase requires linear time `O(n)` and it needs to run for each recursion tree level `O(log n)`. Resulting in `O(n log2 n)`

## Space

The last merge execution (first merge call), the algorithm will need a `temp` array of size `n`, as others calls won't need more memory than this, we can assume the space complexity is `O(n)`. The algorithm allocates memory for other calls, but it won't exist at the same time.