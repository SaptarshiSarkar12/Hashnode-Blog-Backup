---
title: "Mastering Linear Search: Learn the Essentials of This Core Algorithm"
seoTitle: "Unlocking the Basics: A Comprehensive Guide to Linear Search Algorithm"
seoDescription: "Master the basics of Linear Search with this guide covering its implementation, time, and space complexity for efficient algorithm understanding"
datePublished: Sun Aug 03 2025 18:06:02 GMT+0000 (Coordinated Universal Time)
cuid: cmdvzst4d000b02le6o1jhfdj
slug: mastering-linear-search
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1754204891987/50de7e69-ee30-4007-9f5e-47a6401cf438.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1754205160450/1e448447-5bfc-4dd5-b044-70b35d7996db.png
tags: java, dsa, leetcode, linearsearch, search-algrithms

---

Among the various search algorithms, **Linear Search** stands out as the most fundamental. In this article, we will delve into the workings of Linear Search and break down its implementation step by step.

## What is Linear Search?

**Linear Search** is a simple search algorithm that examines each element in a list one by one until it finds the desired element or reaches the end of the list. It doesn't need the data to be sorted.

## How does it work?

Let’s use the array below as an example and say we need to search for the number **63**.

![An array of 6 numbers](https://cdn.hashnode.com/res/hashnode/image/upload/v1752987939733/e37d1935-3f9c-4870-9cf0-b9e923dca8ec.png align="center")

The algorithm will first check the first element, **80**.  
**The index pointer will ask**: “Is 80 the number we need?”  
**The algorithm responds**: “No, it’s not!”

The index pointer moves to the next element, **14**.  
**The pointer asks**, “Is 14 the number we’re looking for?”  
**The algorithm replies**, “No.”

It will then move to the next element, **15**.  
**The pointer asks again**, “Is 15 the number we want?”  
**The algorithm responds**, “No, it isn’t!”

It then moves to the next number, **63**.  
**The pointer asks**, “Is 63 our desired number?”  
**The algorithm responds**, “Yes, it is,” and returns the **index of the number**.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1752989316967/62d49e4f-e60c-441e-8833-ac15ccf29cee.png align="center")

In some case, if the element is **not found**, we can return **\-1** as it is an invalid index.  
As we go through the array, we are basically using either a for loop or a for-each loop (also known as an *enhanced for* loop).

## Time Complexity

We have two scenarios — the best and the worst cases.

### Best Case

The best case happens when the element we're looking for is the **first one** in the array.  
The algorithm finds the required element at the first position, resulting in the fastest possible search time. The time complexity in this situation is **O(1)** (constant).

### Worst Case

The worst case occurs when the element we’re searching for is **not present** in the whole array.  
The algorithm has to traverse the whole array, checking each element one by one until it reaches the end. The time complexity in this situation is **O(N)**, where **N** is the size of the array.

## Space Complexity

Space complexity is **O(1)** i.e. constant space complexity.  
**Constant space complexity (O(1))** means that the amount of memory the algorithm uses does **not grow** with the size of the input. No matter how big the input gets, the algorithm uses the **same fixed amount of space**.

## Example code

Here is a simple Java code for the **linear search algorithm**:

```java
public class Main {
    public static void main(String[] args) {
        int[] nums = {52, 89, 12, 1, 65, 34, 90, -29, -83, -11};
        int target = 90;
        int index = linearSearch(nums, target);
        System.out.println("Index of " + target + " is: " + index);
    }

    // search in the array and return the index of the element if found, otherwise return -1
    private static int linearSearch(int[] arr, int target) {
        if (arr == null || arr.length == 0) {
            return -1; // Return -1 if the array is null or empty
        }

        // Iterate through each element in the array
        for (int index = 0; index < arr.length; index++) {
            // Check if the current element equals the target
            int element = arr[index];
            if (element == target) {
                return index; // Return the index if the element is found
            }
        }
        return -1; // Return -1 if the target is not found in the array
    }
}
```

## Linear Search Techniques

### Linear Search in a Given Range

Suppose we want to find the number **63** in the same array, but only if it exists within the index range of 2 to 4, inclusive.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1753024859915/af883211-f4b0-4726-b220-43d180f3590b.png align="center")

In this case, the loop will *start* at **index 2** and *end* at **index 4**. It will check each element in that range until it either finds the desired element or reaches the end of the loop.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1753025397287/d973d3f8-8c4c-43c5-884f-3453628f2613.png align="center")

Below is an example of searching within a specific range of an array using this algorithm:

```java
public class SearchInRange {
    public static void main(String[] args) {
        int[] arr = {18, 12, -7, 25, 31, 8, 0, 19};
        int target = 8;
        System.out.println(linearSearchInRange(arr, target, 2, 6));
    }

    private static int linearSearchInRange(int[] arr, int target, int start, int end) {
        if (arr == null || arr.length == 0 || start < 0 || end >= arr.length || start > end) {
            return -1; // Handle invalid input
        }

        for (int index = start; index <= end; index++) {
            if (arr[index] == target) {
                return index; // Target found, return index
            }
        }
        return -1; // Target not found in the specified range
    }
}
```

### Linear Search in a 2D Array

Let’s consider the following 2D Array:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1753030001803/608b0c46-aa0f-4a22-8a9a-1630cdeaa254.png align="center")

Clearly, we will need two loops—one to go through each row and another to iterate over each element within those rows. Then, we’ll compare those elements with the target. If it matches, we’ll return it.

Here's a simple code example of how to perform a linear search on a 2D array:

```java
import java.util.Arrays;

public class SearchIn2DArray {
    public static void main(String[] args) {
        int[][] arr = {
            {80, 14, 15, 63},
            {12, 45, 67},
            {34, 78, 90, 11, 22, 33},
            {44, 54, 62, 83, 59}
        };
        int target = 90;
        int[] result = searchIn2DArray(arr, target);
        System.out.println("Location of " + target + " is: " + Arrays.toString(result));
    }

    private static int[] searchIn2DArray(int[][] arr, int target) {
        for (int row = 0; row < arr.length; row++) {
            for (int col = 0; col < arr[row].length; col++) {
                if (arr[row][col] == target) {
                    return new int[] {row, col};
                }
            }
        }
        return new int[] {-1, -1};
    }
}
```

## Conclusion

In conclusion, Linear Search is a simple algorithm that is easy to understand and implement. While not the most efficient for large datasets, it is useful for basic search operations. Whether searching in a range or a 2D array, Linear Search offers a clear method for finding elements. Its fundamental principles are the basis for more advanced search techniques.

⭐ Check out the [DSA](https://github.com/SaptarshiSarkar12/DSA) GitHub repo for more code examples.