---
title: "Everything You Need to Know About Binary Search"
seoTitle: "Binary Search Explained: A Comprehensive Guide"
seoDescription: "Learn binary search algorithm with this comprehensive guide on its principles, applications, and how it compares to other search methods"
datePublished: Sat Sep 20 2025 11:31:24 GMT+0000 (Coordinated Universal Time)
cuid: cmfs6u6xp000502lbelas1ry3
slug: everything-you-need-to-know-about-binary-search
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1758367075000/a1d1a5c4-64e5-4a2e-b17a-744c82901b2b.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1757760003963/1ed8ead8-519f-4afc-b002-117933019322.png
tags: java, dsa, leetcode, binary-search-algorithm, search-algorithms

---

Binary search is a cornerstone of efficient searching techniques, particularly when dealing with large datasets. Its power lies in its ability to drastically cut down the number of comparisons needed to locate an element, thanks to its **divide-and-conquer** approach. This article will guide you through the principles of binary search, its practical applications, and how it stands out from other search algorithms.

## What is Binary Search?

Binary Search is an efficient algorithm used to find the position of a target element in a **sorted array**. It works by repeatedly **dividing the search space in half**, significantly reducing the number of comparisons required.

## How does it work?

Suppose we have a sequence of **N elements** stored in an array. If the sequence is **unsorted**, the standard approach is to examine every element one by one until we either find the target or reach the end of the dataset. This method is commonly known as [**Linear Search**](https://saptarshisarkar.hashnode.dev/mastering-linear-search) (or Sequential Search).

When the sequence is sorted, a more efficient **binary search** algorithm can be used.  
If we consider an arbitrary element in a sequence sorted in increasing order with the value **m**, we can be sure that all elements prior to that have values *less than or equal to* ***m***, and all elements after it have values *greater than or equal to* ***m***. Now, the search area is divided into **two parts** and based on the **target number** (the one we're looking for), we can choose to search in one of these regions.

Let’s consider the array below for a deeper understanding of its working.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1754414618652/2c7f7444-74c0-4aca-81f0-f82633e1a3d3.png align="center")

Suppose we need to look for the **number 81**.

Let `start` and `end` represent start and end indices initially set to `0` and `n-1` (where `n` is the size of the array) respectively.

First the algorithm will find the middle element of the array. Let `m` represent the index of the middle element of the array. Then `m` will be the integral value of half of the sum of start and end indices.  
Mathematically, we can write 👇

$$m = floor(\frac{start + end}{2})$$

Then comes three cases,

1. If the target equals the middle element, then we have found the item we’re looking for and we return it.
    
2. If the target element is less than the middle element, then we’ll need to search again in the first half of the array (i.e. left side of the middle element) as the array is in ascending order.
    
3. If the target element is greater than the middle element, then we’ll need to search again in the second half of the array (i.e. right side of the middle element).
    

In the example, `start` corresponds to `0` index and `end` corresponds to index `7`. So, `m` will be `3`.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1757503966410/2ae5b29e-4bca-4f0f-a491-25ed163103dd.png align="center")

In the first iteration, as 61 is less than our target element 81, we’ll need to search in the right side of 61. So, now our search space will become 👇

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1757504439616/ae166fa8-690e-4087-a8c5-66e1600a40cc.png align="center")

`start` will become `4` (because we’ve already checked that **61 is not equal to 81**). Now, `m` will become `5`.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1757504550993/485448b4-1525-4ac2-9d65-8faf8a4945af.png align="center")

The middle element, 81, is equal to the target element. Therefore, the loop will stop here, returning the index of the target element in the array.

## Time Complexity

We have two scenarios here — the best case and the worst cases.

### Best Case

Let's say we have an array where the middle element is the same as the target. In this case, the algorithm will make just one comparison, which is the best-case scenario. So, the time complexity in this case will be **O(1)**.

### Worst Case

Suppose we have an array with **N elements** where the target element is not present. So, the algorithm will proceed as follows:

The algorithm will first find the middle element of the entire array. Let’s say that the target element is greater than the middle element, so the search space will be reduced to **N/2** (right side of the middle element).

Again, suppose the target element is to the left of the new middle element. The search space will then shrink to **N/4**, then to **N/8**, and so on. Eventually, only one element will remain, making the final search space **1**. That last element will either match the target element, or it won't, both being worst-case scenarios.

We can visualize the number of comparisons made in each iteration using the following diagram. Let the Kth comparison be the last one.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1757653025436/37322343-d461-4d95-b22d-63aae4c33b15.png align="center")

For the **0th comparison**, the search space is **N** which can be written as \\(\frac{N}{2^0}\\).

For **1st comparison**, **N/2** can be written as \\(\frac{N}{2^1}\\).

Similarly, **N/4** can be written as \\(\frac{N}{2^4}\\).

and so on. Following the same pattern, we can write **1** as \\(\frac{N}{2^k}\\)

Therefore,

$$N = 2^k$$

Taking \\(log\\) on both sides,

$$\begin{align} log\ N = log\ 2^k \\ \Rightarrow log\ N = k\ *\ log\ 2 \\ \therefore k = log_{2}\ (N) \end{align}$$

Hence, total number of comparisons in the worst-case scenario is \\(log\ N\\). So, the time complexity is **O(log N)**. Remember, constants are ignored in time complexity.

## Example Code

An example code in Java is shown below.

We cannot use the \\(mid = \frac{start\ +\ end}{2}\\) formula because `int` has a **fixed size limit**, and the value of `start + end` may **exceed** the maximum value supported by `int`. Therefore, we use the safer alternative:

$$mid = start\ +\ \frac{end\ -\ start}{2}$$

```java
public class Main {
    public static void main(String[] args) {
        int[] arr = {-87, -58, -23, 2, 5, 63, 94, 99, 135, 189};
        int target = 94;
        int index = binarySearch(arr, target);
        System.out.println("Index of " + target + " is " + index);
    }

    // return the index
    // return -1 if the element does not exist
    static int binarySearch(int[] arr, int target) {
        int start = 0;
        int end = arr.length - 1;

        while (start <= end) {
            int middle = start + (end - start) / 2;
            if (target < arr[middle]) {
                end = middle - 1;
            } else if (target > arr[middle]) {
                start = middle + 1;
            } else {
                return middle;
            }
        }
        return -1;
    }
}
```

## Order Agnostic Binary Search

Currently, we have assumed that the array is sorted in ascending order. Now, we will explore an order-agnostic binary search algorithm. This algorithm first checks the order of the sorted array and then performs the search accordingly. Time complexity will remain the same.

The simplest way to check the order of the array is to check the first and the last elements of the array and compare between them.

### Example Code

Here’s a sample code for order agnostic binary search algorithm:

```java
public class OrderAgnosticBS {
    public static void main(String[] args) {
        int[] arr1 = {-87, -58, -23, 2, 5, 63, 94, 99, 135, 189};
        int[] arr2 = {157, 100, 65, 52, 37, 24, 18, -4, -36, -58, -88};
        int target1 = 94;
        int target2 = 65;
        int index1 = orderAgnosticBS(arr1, target1);
        System.out.println("[arr1]:  Index of " + target1 + " is " + index1);
        int index2 = orderAgnosticBS(arr2, target2);
        System.out.println("[arr2]: Index of " + target2 + " is " + index2);
    }

    static int orderAgnosticBS(int[] arr, int target) {
        int start = 0;
        int end = arr.length - 1;

        // find whether the array is sorted in ascending or descending order
        boolean isAscending = arr[start] < arr[end];

        while (start <= end) {
//            int middle = (start + end) / 2; // The value "start + end" might exceed the maximum possible integer value
            int middle = start + (end - start) / 2;

            if (arr[middle] == target) {
                return middle;
            }

            if (isAscending) {
                if (target < arr[middle]) {
                    end = middle - 1;
                } else {
                    start = middle + 1;
                }
            } else {
                if (target > arr[middle]) {
                    end = middle - 1;
                } else {
                    start = middle + 1;
                }
            }
        }
        return -1;
    }
}
```

## Searching in Matrix

Suppose in the matrix below, we need to search for the number **98**. The simplest way is to go through each element of the matrix by iterating through each row and column using two `for` loops.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1758343010110/126d760c-86e9-4760-8fd0-4996534707c9.png align="center")

After comparison, we’ll easily get the answer as `[1, 3]`. In the worst case, the maximum number of comparisons made will be **M\*N** (where **M** is the *number of rows* and **N** is the *number of columns*). The time complexity would be **O(M\*N)**.

If a matrix is given such that it is sorted **row wise and column wise**, we should think of minimizing the search space in some logical ways.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1758350555989/193e2852-21a9-4483-ae65-5e03327eb779.png align="center")

Let’s say we’re looking for the number **32** in the above array.

We’ll take the smallest element (here `2`) as the **lower bound** and the largest element in the first row as the **upper bound** (here `23`).

Let’s look for the possible cases to eliminate rows and columns to minimize the search space as much as possible:

**Case 1**: If element is equal to the target, then answer is found.

**Case 2**: If the element is less than the target, then all the numbers to the left of that element will also be less than the target. So, that particular row is ignored. As **18** &lt; **32**, so 1st row is ignored. We then move to **2nd row** at `[2, 1]` position (as last column is eliminated in **case 3**) where we found the target element.

**Case 3**: If element is greater than target, column will get reduced. Let’s say if our target is less than **23**, then the target will also be less than each of the elements in the last column. So, the last column will be ignored.

Remember, we’ll start searching from **first row** and **last column** and keep running the loops until **row number &lt; length** and **column number &gt;= 0**.

### Time Complexity

The **row counter** is going **from 0 to N-1** and the **column counter** is going **from N-1 to 0** (where **N** is the total number of rows/columns in the given **square matrix**). In the worst case, each of the counters will move N times. So, the total number of comparisons made is equal to 2N. Hence, time complexity is **O(N)**.

### Space Complexity

As we are not utilising any auxiliary space, so the space complexity would be **O(1)**.

## Searching in a Sorted Matrix

When all the elements are strictly sorted in a matrix, we can think of applying a binary search. An Example of such a matrix is given below.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1758359378015/86ce2b2b-dbdb-4a89-a041-b1b8cd52a17d.png align="center")

Let’s say our target element is **16**.

We can take the middle column and perform binary search on it to **reduce the number of rows to be searched** (or middle row to **reduce the number of columns to be searched**).

Hence, we’ll be first applying binary search on **2nd column**. Our **mid** element will be **32**.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1758363181960/fda07f69-fb4d-4a0a-98c2-9c9148e2b04b.png align="center")

As **32 &gt; target element** `16`, so the **last 2 rows** will be **ignored** as those have elements greater than 32 *and therefore greater than* ***16***.

There will be three cases in binary search:

1. If the element is equal to the target, we've found our answer.
    
2. If the element &gt; target, ignore rows below that element.
    
3. If element &lt; target, all rows above it will get ignored.
    

Remember, there will be two pointers — start and end pointers of row. For example, row-start pointer will be at 0 and row-end will be at 3 indices initially.

In the end, when only two rows will remain, we’ll first check in the mid column’s segment if it contains the required value. In this case, it does so that’s our answer.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1758364369544/96fd103b-c9d6-4f07-ae62-8b3c3268d426.png align="center")

Let’s say the **target element** was `18`, then we will need to apply simple binary search in each of the four parts as shown in white coloured shapes below. This is because each of the parts are sorted.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1758364622556/c24e390b-c3d4-4948-af3a-b9735733a06e.png align="center")

### Time Complexity

We’re making comparisons column wise first (by binary search), so the number of comparisons there is **log(N)** where **N** is the length of the column. Then, let’s say in the worst case, we apply binary search in rows up to size **M**. So, number of comparisons will be **log(M)**.

Hence, time complexity would be **O(log (N) + log (M))**.

### Space Complexity

As we are not using any auxiliary space, so space complexity is **O(1)**.

## Conclusion

I hope this article has provided you with a clear understanding of binary search and its significance in efficient data searching. Whether you're a beginner or an experienced programmer, mastering binary search can greatly enhance your problem-solving skills and optimize your algorithms. Keep exploring and practicing harnessing the full potential of this fundamental algorithm in your coding journey. Thank you for reading, and happy coding!

⭐ Check out the [**DSA**](https://github.com/SaptarshiSarkar12/DSA) GitHub repo for more code examples.