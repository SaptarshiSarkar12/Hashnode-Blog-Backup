---
title: "How Insertion Sort Works: Simplified Explanation"
seoTitle: "Simplified Guide to Insertion Sort"
seoDescription: "Learn how insertion sort works, its time complexity, and why it's ideal for small datasets and nearly sorted arrays"
datePublished: Sat Nov 29 2025 06:55:41 GMT+0000 (Coordinated Universal Time)
cuid: cmijxt9bl000002js9mz59e7w
slug: how-insertion-sort-works-simplified-explanation
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1764399290698/82f20f44-2cf6-4e70-8b8a-740667072c64.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1764399277526/8946ad1e-7845-4226-8b61-b489d63f6207.png
tags: java, insertion-sort, dsa, sorting-algorithms, dsawithkunal, dsainjava

---

Insertion sort is a simple comparison-based sorting algorithm that sorts by repeatedly inserting elements into their correct position. Let's explore how it works in detail.

## What is Insertion Sort?

[Insertion Sort](https://en.wikipedia.org/wiki/Insertion_sort) is a [**comparison sort**](https://en.wikipedia.org/wiki/Comparison_sort) algorithm. It divides the array into two parts: the sorted part and the unsorted part. It repeatedly inserts each element from the unsorted part into its correct position in the sorted part of the array.

## How does it work?

Let’s take the following array as an example. We need to sort it in ascending order.

![example array](https://cdn.hashnode.com/res/hashnode/image/upload/v1764337762308/1378e868-1eca-43ad-aac4-4aecd3595b78.png align="center")

The insertion sort algorithm uses two loops: one controls **the number of passes** (or traversals) through the array, and the other **compares adjacent elements** and performs swap if needed, starting from the first element of the unsorted section. Let variable `i` control the **number of passes** and variable `j` control the **comparison of adjacent elements**. As `i` increases, the **sorted section grows**, and `j` helps place each element in its correct position within the sorted section.

<div data-node-type="callout">
<div data-node-type="callout-emoji">💡</div>
<div data-node-type="callout-text">Since we are sorting in ascending order, the sorted part of the array is on the left side.</div>
</div>

![image of example array showing the i and j pointers along with indices of each element](https://cdn.hashnode.com/res/hashnode/image/upload/v1764338538770/9ccdc74c-055e-4369-8059-7eea26e7d029.png align="center")

Initially, `i` should start from **index 0**. The variable `j` takes the value `i+1` which in the initial case is **index 1**.

As the sorted region lies behind the initial value of `j` in each pass, the algorithm compares the `j`th element with the `j-1`th element.  
It will check: is **9** less than **3**? No, it isn’t. So, it will get swapped.

![array after the first swap is shown along with the change of pointer values](https://cdn.hashnode.com/res/hashnode/image/upload/v1764339937848/973dfbe1-2fce-44bb-bcfc-12d94f9cab51.png align="center")

After the swap, the value of `j` decreases by a unit. As the `j-1`th element is undefined (error will be thrown if we try to access that element), so `j` should always be greater than `0`.

Now, in the second pass, `i` increases to **1**. `j` takes the value of `2`.

![Image showing array with i and j pointers for the second pass and the sorted portion of it is indicated](https://cdn.hashnode.com/res/hashnode/image/upload/v1764344362579/d1475935-3e07-4b3f-ab0b-493084a6a6f7.png align="center")

Now, the algorithm checks: is **9** less than **6**? No, it is not. So, they will be swapped.

![array after the first swap in the second pass is shown along with the change of values of pointer variables](https://cdn.hashnode.com/res/hashnode/image/upload/v1764344426715/d168a420-6055-4bf7-8c0e-863d59c1e43e.png align="center")

The value of `j` changes to **1**. The algorithm now checks: is **3** less than **6**? Yes, it is. So, no swap operation will be performed.

Now, the third pass starts. The value of `i` changes to **2** and `j` becomes **3**.

![Image showing array with i and j pointers for the third pass and the sorted portion of it is indicated](https://cdn.hashnode.com/res/hashnode/image/upload/v1764344819083/a5d4da37-2844-4310-8407-c30a91424206.png align="center")

Now, the algorithm checks: is **9** less than **10**? Yes, it’s. So, no swap operation will be performed.

As we know, the **part of the array** on the **left side of** `j` is **already sorted** at the **beginning of each pass**. Therefore, it's unnecessary to check all the way to the leftmost end of the array. If the desired order is found between adjacent elements during comparison, the **internal loop can exit** for that pass.

Now, starting with the fourth pass, the value of `i` becomes **3** and that of `j` becomes **4**.

![Image showing array with i and j pointers for the fourth pass and the sorted portion of it is indicated](https://cdn.hashnode.com/res/hashnode/image/upload/v1764345104581/21dcd638-3f03-4ae3-a670-3663d92f8bf8.png align="center")

The algorithm now checks: is **10** less than **1**? No, it isn’t. So, they will be swapped.

![array after the first swap in the fourth pass is shown along with the change of values of pointer variables](https://cdn.hashnode.com/res/hashnode/image/upload/v1764373431440/786949dd-f592-4a02-93e5-45d20bf4ef47.png align="center")

The value of `j` changes to **3**. Now, it checks: is **9** less than **1**? No, it isn’t. So, they’ll be swapped.

![array after the second swap in the fourth pass is shown along with the change of values of pointer variables](https://cdn.hashnode.com/res/hashnode/image/upload/v1764374049930/ec82e24e-3b27-43be-9dd0-5005b0896a06.png align="center")

`j` is now at **index 2**. It checks: is **6** less than **1**? No, it isn’t. So, they get swapped.

![array after the third swap in the fourth pass is shown along with the change of values of pointer variables](https://cdn.hashnode.com/res/hashnode/image/upload/v1764374470145/cbc9ba6e-2f36-4eb7-b26c-d3fab8933a1d.png align="center")

The value of `j` decreases to **1**. Now, it checks: is **3** less than **1**? No, it isn’t. So, they get swapped.

![array after the fourth swap in the fourth pass is shown along with the change of values of pointer variables](https://cdn.hashnode.com/res/hashnode/image/upload/v1764375121372/e69ae861-b54b-4226-9eb1-9b5a6ca39bc6.png align="center")

Now, the internal loop exits. As `j` takes the value `i+1` and **index 5** does not exist, so the maximum value of `i` should be **3**. In general, `i` must be less than **N - 1** where **N** is the length of the array.

Our array is finally sorted! 😃

![Image of the final sorted array](https://cdn.hashnode.com/res/hashnode/image/upload/v1764375491533/2f5ca555-fab2-4b44-82fb-e80e5cd06308.png align="center")

## Time Complexity

There are two possible scenarios: the **best case** and the **worst case**.

### Worst Case

The worst case occurs when the array is sorted in the reverse order. Let’s try to find out the total number of comparisons made.

* In the **1st pass**, only **1** comparison is made.
    
* In the **2nd pass**, **2** comparisons are made.
    
* …
    
* In the `N-1`th pass, `N-1` comparisons are made.
    

So, the total number of comparisons made is:

$$\sum_{i=1}^{N-1} i = \frac {N*(N-1)}{2} \\ = \frac {N^2 - N}{2}$$

Hence, the time complexity is **O(N²)** as constants are cancelled, and less dominating terms are removed.

### Best Case

The best case occurs when the **array is already sorted in the desired order**. In that case, there will be **utmost 1 comparison made in each pass** because the **internal loop will break** once it finds that the desired order is followed by the adjacent elements while comparing them. Therefore, total number of comparisons made is \\(N-1\\) where \\(N\\) is the size of the array.

Hence, the time complexity in this scenario is **O(N)**.

## Space Complexity

As the insertion sort algorithm is an in-place sorting algorithm, it does not use any auxiliary space. Hence, its space complexity is **O(1)**.

## Stability

The insertion sort is a **stable sorting algorithm** as the original order of **the equal elements** (or the duplicate elements) is maintained in the final sorted array.

## Uses of Insertion Sort

Insertion sort is the most efficient sorting algorithm for small arrays because it is **adaptive**. **Adaptive** means that for smaller values of **N**, the number of comparisons made are reduced and number of swaps performed is also less compared to **bubble sort**.

It works better when the array is nearly sorted. Hence, it is often used in [hybrid sorting algorithms](https://en.wikipedia.org/wiki/Hybrid_algorithm) like [TimSort](https://en.wikipedia.org/wiki/Timsort) and [IntroSort](https://en.wikipedia.org/wiki/Introsort).

## Example Code

```java
import java.util.Arrays;

public class Main {
    public static void main(String[] args) {
        int[] arr = {9, 3, 6, 10, 1};
        insertionSort(arr);
        System.out.println(Arrays.toString(arr));
    }

    static void insertionSort(int[] arr) {
        for (int i = 0; i < arr.length - 1; i++) {
            for (int j = i + 1; j > 0; j--) {
                if (arr[j] < arr[j - 1]) {
                    swap(arr, j, j-1);
                } else {
                    break;
                }
            }
        }
    }

    static void swap(int[] arr, int first, int second) {
        int temp = arr[first];
        arr[first] = arr[second];
        arr[second] = temp;
    }
}
```

## Conclusion

Insertion sort is a straightforward and efficient algorithm for sorting small arrays. Because of its adaptive nature and its stability, it performs well on nearly sorted arrays. Understanding insertion sort provides a solid foundation for learning more complex sorting techniques.

⭐ Check out the [**DSA**](https://github.com/SaptarshiSarkar12/DSA) GitHub repo for more code examples.