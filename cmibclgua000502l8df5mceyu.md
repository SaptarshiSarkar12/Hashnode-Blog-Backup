---
title: "A Beginner's Guide to Bubble Sort Algorithm"
seoTitle: "Bubble Sort Algorithm: A Beginner's Guide"
seoDescription: "Learn bubble sort, a simple algorithm for sorting elements by comparing and swapping adjacent items until the list is ordered"
datePublished: Sun Nov 23 2025 06:39:37 GMT+0000 (Coordinated Universal Time)
cuid: cmibclgua000502l8df5mceyu
slug: a-beginners-guide-to-bubble-sort-algorithm
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1763879814667/f80a0762-3f5e-4c52-b921-ec474b042243.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1763879881660/4057ace5-ace8-4fa7-ac2c-79075c904982.png
tags: java, dsa, leetcode, bubble-sort, sorting-algorithms

---

**Bubble sort** (also called as **Sinking Sort** and **Exchange Sort**) is a straightforward sorting algorithm that operates by repeatedly comparing and swapping adjacent elements if they are in the wrong order.

## What is Bubble Sort?

[Bubble Sort](https://en.wikipedia.org/wiki/Bubble_sort) is a [comparison sort](https://en.wikipedia.org/wiki/Comparison_sort) algorithm that organizes elements in a list by repeatedly comparing and swapping adjacent elements if they are in the wrong order. It is named for the way smaller elements "bubble" to the top of the list. The passes through the list are repeated until no swaps have to be performed during a pass.

## How does it work?

Let’s take the following array as an example. We need to sort it in ascending order.

![Sample array for demonstrating how bubble sort works](https://cdn.hashnode.com/res/hashnode/image/upload/v1763683301773/eb882f87-fdfb-4187-8f02-434eea945252.png align="center")

As the bubble sort algorithm is a comparison sort algorithm, in each pass (or traversal through the array), it will compare each pair of adjacent elements. We’ll start with the first two elements.

The algorithm checks: is **6** less than **2**? No. Then, swap **6** and **2**.

![First swap shown in the sample array](https://cdn.hashnode.com/res/hashnode/image/upload/v1763683793759/566ee61d-40f0-4534-9a8f-f46a0dd9918f.png align="center")

Then, the next pair of elements are checked. The algorithm asks: is **6** less than **5**? No, it’s not. So, it will swap **6** and **5**.

![Second swap shown](https://cdn.hashnode.com/res/hashnode/image/upload/v1763684045150/ac739b6d-1d38-46cf-b908-f28cda33bcc5.png align="center")

The algorithm picks the next pair of adjacent elements and checks: is **6** less than **8**? Yes! Then, it’ll move to the next pair.

The algorithm now checks: is **8** less than **3**? No, isn't. So, it’ll swap **8** and **3** elements.

![The last swap in the first pass is shown](https://cdn.hashnode.com/res/hashnode/image/upload/v1763684364246/ed82ea8d-15e8-417c-ba9c-7530045d437e.png align="center")

The first pass is now completed. It will go for the next pass.

<div data-node-type="callout">
<div data-node-type="callout-emoji">💡</div>
<div data-node-type="callout-text">Notice that the <strong>largest element</strong> of the list comes at the <strong>end of the list </strong>in the first pass.</div>
</div>

In the second pass, we’ll again start with the first two pair of elements. The algorithm checks: is **2** less than **5**? Yes, it is. Then, it checks: is **5** less than **6**? Yes!

Then, **6** less than **3**? No! So, perform swap.

![First swap in the second pass is shown](https://cdn.hashnode.com/res/hashnode/image/upload/v1763685342320/4abf63f1-da5c-46e0-a71b-f279603d0d14.png align="center")

Next, the algorithm checks: is **6** less than **8**? Yes, it is. So, it will go for the next pass.

<div data-node-type="callout">
<div data-node-type="callout-emoji">💡</div>
<div data-node-type="callout-text">We notice that in the <strong>2nd pass</strong>, the <strong>2nd largest element </strong>of the list goes to the <strong>2nd last position</strong> of the list.</div>
</div>

In the third pass, the algorithm starts by again checking the first two pair of elements. It checks: is **2** less than **5**? Yes! Next, it checks: is **5** less than **3**? No, perform swap.

![First swap in the third pass is shown](https://cdn.hashnode.com/res/hashnode/image/upload/v1763685722299/2e1924da-b144-4e23-baaa-5d93e94b9833.png align="center")

Then, the algorithm checks: is **5** less than **6**? Yes!  
Next, it checks: Is **6** less than **8**? Yes!

<div data-node-type="callout">
<div data-node-type="callout-emoji">💡</div>
<div data-node-type="callout-text">We again notice that the <strong>third largest element</strong> of the list comes at the third last position of the list.</div>
</div>

The array is finally sorted 😀!

![Final sorted array is shown](https://cdn.hashnode.com/res/hashnode/image/upload/v1763686998652/e5fe507b-c0c1-4045-99fb-e19c8ceb4813.png align="center")

### Reducing redundant checks

In the subsequent passes, we notice that rightmost part of the array is getting gradually sorted. So, in the next pass, there is **no need** to check that **sorted part of the array**.

![Sorted parts of array are shown in subsequent three passes](https://cdn.hashnode.com/res/hashnode/image/upload/v1763687986696/9939580c-12dc-4768-bcd7-245aff73b7f2.png align="center")

Notice that in the **first pass**, one element gets sorted; in the **second pass**, 2 elements are sorted and so on. So, in the `n-1`***th* pass**, only the first element will remain. Hence, we need to run the loop (for passes) `n-1` times.

### How does the optimized algorithm work?

The algorithm has two loops: the **outer loop** for the number of passes and the **inner loop** which compares each pair of adjacent elements and perform swap if required.

We start with **i = 0** (the ***first*** pass). The pointer variable **j** goes from 0 till the last element.

![The range of possible values of the pointer variable j is shown in the first pass](https://cdn.hashnode.com/res/hashnode/image/upload/v1763856419859/b514d9b1-d736-4058-a737-542a3b7dccc8.png align="center")

Then for **i = 1** (the *second* pass), *j* runs from 0 to 3rd index as the last element is the largest element (so last element is “sorted”).

![The range of possible values of the pointer variable j is shown in the second pass](https://cdn.hashnode.com/res/hashnode/image/upload/v1763857068665/81324dee-27d9-4ee7-b9bd-7550b532ccf8.png align="center")

Now for **i = 2** (the *third* pass), *j* runs from 0 to 2nd index as the last 2 elements are sorted.

![The range of possible values of the pointer variable j is shown in the third pass](https://cdn.hashnode.com/res/hashnode/image/upload/v1763857392097/e1bf1192-9cbd-4e89-a32e-d9c1d9d5b2a0.png align="center")

Now, for **i = 3** (the *fourth* pass), j runs from 0 to 1st index as the rest of the elements are sorted. On comparing the **first 2 elements** of the array (the **only** remaining elements), the algorithm finds that they are sorted. Hence, the algorithm ends here.

Generalizing, we get the following results:

* counter variable ***i*** runs from **0** till **n - 1**
    
* pointer variable ***j*** runs from **0** till **n - i - 1**
    

where **n** is the length of the array.

## Space Complexity

As we are not taking up any extra space (like creating extra array or variables), so space complexity of bubble sort is **O(1)** means **constant space complexity**. Hence, bubble sort is an **in-place sorting algorithm**.

## Time Complexity

We have two scenarios here: the **Best Case** and the **Worst Case**.

### Best Case

The best case happens when the array is sorted in the desired order. Now, how do we know if the array is sorted? In the first pass, if no swap operation is performed, then it means that the array is sorted and the algorithm can stop. Hence, total number of comparisons made = N - 1. So, **time complexity** of bubble sort is **O(N)**.

<div data-node-type="callout">
<div data-node-type="callout-emoji">💡</div>
<div data-node-type="callout-text">Remember, constants are ignored in time complexity because want to find a <strong>mathematical relationship between time and length of inputs</strong> and are not interested in calculating the exact time taken by the algorithm.</div>
</div>

### Worst Case

The worst case occurs when the array is sorted in the reverse order. Let’s try to find the total number of comparisons made in this case:

In an array of N elements,

* In the 1st pass, N - 1 comparisons are made.
    
* In the 2nd pass, N - 2 comparisons are made.
    
* …
    
* In the `N - 1`th pass, 1 comparison is made.
    

So, the total number of comparisons is:

$$\sum_{i = 1}^{N-1} (N - i) = N*(N-1) \ - \frac{N*(N-1)}{2} \\ = \frac{N*(N-1)}{2} \\ = \frac{N^2-N}{2}$$

Therefore, time complexity is **O(N²)** as constants are cancelled, and less dominating terms are removed.

## Stability of Sorting Algorithm

The stability of a sorting algorithm refers to how it handles the **order of equal** (or duplicate) elements. If the algorithm maintains the original order of equal elements in the final sorted array, it is called a **stable sorting algorithm**. Bubble Sort algorithm is one such example.

## Example Code

```java
import java.util.Arrays;

public class Main {
    public static void main(String[] args) {
        int[] arr = {6, 2, 5, 8, 3, -45, 0, 34, 12};
        bubbleSort(arr);
        System.out.println("Sorted array: " + Arrays.toString(arr));
    }

    static void bubbleSort(int[] arr) {
        boolean swapped = false;
        // run the outer loop for n-1 passes
        for (int i = 0; i < arr.length - 1; i++) {
            // In each subsequent pass, the largest element comes at the last respective index
            for (int j = 1; j < arr.length - i; j++) {
                // swap if the item is smaller than the previous item
                if (arr[j] < arr[j - 1]) {
                    int temp = arr[j];
                    arr[j] = arr[j - 1];
                    arr[j - 1] = temp;
                    swapped = true;
                }
            }

            // if you did not swap for a particular pass, it means the array is sorted
            if (!swapped) {
                break;
            }
        }
    }
}
```

## Conclusion

Bubble Sort is a basic yet important sorting algorithm that helps explain how sorting works through comparing and swapping elements. Although it is not very efficient for large datasets because of its O(N²) time complexity in the worst case, it is a great learning tool for beginners to understand the basics of sorting algorithms. Its stability and in-place sorting make it useful for small datasets or when memory usage is a concern.

⭐ Check out the [**DSA**](https://github.com/SaptarshiSarkar12/DSA) GitHub repo for more code examples.