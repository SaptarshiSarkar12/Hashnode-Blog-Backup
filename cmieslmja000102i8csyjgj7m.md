---
title: "Mastering Selection Sort: A Simple Explanation"
seoTitle: "Selection Sort Simplified: Easy Guide"
seoDescription: "Learn the fundamentals of Selection Sort, a simple algorithm to sort arrays by finding and placing smallest or largest elements iteratively"
datePublished: Tue Nov 25 2025 16:30:56 GMT+0000 (Coordinated Universal Time)
cuid: cmieslmja000102i8csyjgj7m
slug: mastering-selection-sort
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1764087887154/4b413ad9-47c6-4a69-9012-44ef0ccb5996.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1764088025406/a2e77917-a52e-4ca7-a27a-18c49d82c6d1.png
tags: java, dsa, leetcode, sorting-algorithms, selection-sort

---

**Selection Sort** is a simple sorting algorithm that repeatedly finds the smallest (or the largest) element from the unsorted part and moves it to its correct position.

## What is Selection Sort?

[Selection sort](https://en.wikipedia.org/wiki/Selection_sort) is a [comparison sort](https://en.wikipedia.org/wiki/Comparison_sort) algorithm. It repeatedly **selects** the smallest or largest element from the unsorted part of the array and swaps it with the element at the appropriate index. This is why it is named **Selection Sort**.

## How does it work?

Let’s take the following array as an example. We need to sort it in ascending order.

![Image of an unsorted array](https://cdn.hashnode.com/res/hashnode/image/upload/v1764044818191/0caf4a5a-81e3-4bb3-9ae2-9387925c2981.png align="center")

The selection sort algorithm finds the **smallest** element of the array at every traversal. Here, the smallest element is **1** so it put **1** at the **first position** (0th index). Hence, it swaps **1** and **9**.

![Image showing swapping of two elements to place the smallest element at the first position](https://cdn.hashnode.com/res/hashnode/image/upload/v1764045690501/3955bcdd-ed40-4007-9aab-338c19204f61.png align="center")

Next, in the following pass, the smallest element is **3**. Its correct index is **1**. Since it is already in the right place, no swap is needed.

![Image showing unsorted part of an array after the 2nd traversal is completed](https://cdn.hashnode.com/res/hashnode/image/upload/v1764046661529/0ff5613f-313f-441e-9fb6-9099f52c994d.png align="center")

Now the next smallest element from the unsorted part of the array is **5**. It must be placed in the 3rd position (**2nd index**). Hence, the algorithm will swap **9** and **5**.

![Image showing swapping in the 3rd traversal](https://cdn.hashnode.com/res/hashnode/image/upload/v1764046925849/c450cf17-f55a-4671-ace8-d0071402eb7f.png align="center")

In the next pass, the **smallest** element of the **unsorted part of the array** is **8**. As **8** is already in its appropriate position, no swap is performed. The last element is not checked because if all the other elements are in their correct positions, then the last element must also be in its correct position.

The array is finally sorted 😃!

![Final sorted array](https://cdn.hashnode.com/res/hashnode/image/upload/v1764047249957/5546d138-5cc6-4ad9-afdc-4146d0e397fb.png align="center")

<div data-node-type="callout">
<div data-node-type="callout-emoji">🗒</div>
<div data-node-type="callout-text">Similar procedure will be followed if we start with the <strong>largest</strong> element.</div>
</div>

## Time Complexity

The algorithm works in two steps:

* Finds the smallest (or the largest) element of the unsorted part of the array
    
* Swap it!
    

For finding the smallest (or the largest) element of the array, **N - 1** comparisons need to be made where **N** is the size of the array.

In the first traversal, **N - 1** comparisons are made. In the second traversal, **N - 2** comparisons are made as one element is already sorted. In the third traversal, **N - 3** comparisons are made and so on. In the last traversal, only **1** comparison will be made.

Hence, total number of comparisons is

$$1 + 2+...+(N-1) \\ = \frac {(N-1)(N-1+1)}{2} \\ = \frac {N(N-1)}{2} \\ = \frac {N^2 - N} {2}$$

Therefore, time complexity is **O(N²)** as constants are cancelled, and less dominating terms are removed.

In both the **worst case** and the **best case**, the time complexity is **O(N²)** as even in the best case, comparisons are made to find the smallest (or the largest) element every time.

## Space Complexity

The space complexity of selection sort algorithm is **O(1)** as no extra space is taken.

## Stability

The **Selection Sort** is not a stable sorting algorithm as it does not maintain the original order of the **equal elements** (or duplicate elements) in the final sorted array as it was present in the original array.

## Example Code

The example code demonstrates two possible implementations of the selection sort algorithm within a single Java file. One method selects the **smallest element** from the unsorted part of the array during each pass, while the other method selects the **largest element**.

```java
import java.util.Arrays;

public class Main {
    public static void main(String[] args) {
        int[] arr = {64, 25, 12, 22, 11};
        selectionSortUsingMaxElement(arr);
        System.out.println("Sorted array: " + Arrays.toString(arr));
        int[] arr2 = {89, 45, 68, 90, 29, 34};
        selectionSortUsingMinElement(arr2);
        System.out.println("Sorted array: " + Arrays.toString(arr2));
    }

    static void selectionSortUsingMaxElement(int[] arr) {
        for (int i = 0; i < arr.length - 1; i++) {
            // find the maximum element in unsorted part of the array and
            // swap it with correct index
            int lastIndex = arr.length - i - 1;
            int maxIndex = getMaxIndex(arr, 0, lastIndex);
            swap(arr, maxIndex, lastIndex);
        }
    }

    static void selectionSortUsingMinElement(int[] arr) {
        for (int i = 0; i < arr.length - 1; i++) {
            // find the smallest number in the unsorted part of the array and
            // swap it with the correct index
            int firstIndex = i;
            int minIndex = getMinIndex(arr, firstIndex, arr.length - 1);
            swap(arr, firstIndex, minIndex);
        }
    }

    private static int getMinIndex(int[] arr, int start, int end) {
        int min = start;
        for (int i = start; i <= end; i++) {
            if (arr[i] < arr[min]) {
                min = i;
            }
        }
        return min;
    }

    private static int getMaxIndex(int[] arr, int start, int end) {
        int max = start;
        for (int i = start; i <= end; i++) {
            if (arr[i] > arr[max]) {
                max = i;
            }
        }
        return max;
    }

    static void swap(int[] arr, int i, int j) {
        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }
}
```

## Conclusion

Selection Sort is a straightforward and intuitive sorting algorithm that is easy to understand and implement. This algorithm is used for small datasets. An advantage of this algorithm over bubble sort is that it requires fewer swaps. It is also an in-place sorting algorithm so can be used where memory usage is a concern.

⭐ Check out the [**DSA**](https://github.com/SaptarshiSarkar12/DSA) GitHub repo for more code examples.