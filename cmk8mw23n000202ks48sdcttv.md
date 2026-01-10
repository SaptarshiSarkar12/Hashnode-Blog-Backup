---
title: "Cyclic Sort Made Simple: Learn the Basics and How It Works"
seoTitle: "Cyclic Sort Basics Explained"
seoDescription: "Learn how the cyclic sort algorithm works to efficiently sort arrays in place with O(n) time complexity"
datePublished: Sat Jan 10 2026 18:23:53 GMT+0000 (Coordinated Universal Time)
cuid: cmk8mw23n000202ks48sdcttv
slug: cyclic-sort-made-simple
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1768069200353/0262d6b0-aeda-402f-a744-9fc6ffec8aa6.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1768069288085/df0bbe5d-a54e-491e-9ac3-93749e38453a.png
tags: java, dsa, leetcode, sorting-algorithms, dsainjava, cyclic-sort

---

Cyclic sort is an in-place and unstable sorting algorithm that is specifically designed to efficiently sort arrays where numbers are in a known range like from **1** to **N**.

## How does it work?

Let’s take the following array as an example. We need to sort it in ascending order.

![Image of sample array](https://cdn.hashnode.com/res/hashnode/image/upload/v1767714428315/10011ed8-db7e-4743-b789-1c23bc3bc3a3.png align="center")

The algorithm works by choosing an element and puts it at its correct index. It starts with the first element.

In the example array, the algorithm chooses the first element **5**. Its correct index is **4**.

![Image of the array showing the position of the control variable and the correct index of the selected element](https://cdn.hashnode.com/res/hashnode/image/upload/v1767717715184/235edfb0-87fa-4408-aec0-7d18d7d6241a.png align="center")

The algorithm swaps **5** with the element at the correct index of **5** i.e. element 2 present at index **4**.

![Image showing the swap operation of the first element with the element at its correct index](https://cdn.hashnode.com/res/hashnode/image/upload/v1767718294780/a8ec9328-2b3d-43d5-a2e6-88cace57c2f2.png align="center")

The algorithm now checks whether the element at the position of the control variable **i** is in its correct position: Is **2** in its correct position? No. So, the control variable will not increment its position.

![Image showing the currently selected element and its correct index](https://cdn.hashnode.com/res/hashnode/image/upload/v1767719119970/d4d1d424-9b79-4e71-a3e9-e750e641a419.png align="center")

The algorithm will swap **2** with **4** (as the correct index of **2** is **index 1**).

![Image showing swap operation of element 2 with element 4](https://cdn.hashnode.com/res/hashnode/image/upload/v1767719277671/c85a966d-231c-4b33-80e3-480dd058a1c2.png align="center")

It will again check: is **element 4** is at its correct index? No, it isn’t. The correct index of **4** is **index 3**.

![Image showing the element 4 as the currently selected element and its correct index 3](https://cdn.hashnode.com/res/hashnode/image/upload/v1767720101615/906f6a9d-1314-4bd4-8953-1861c53aef37.png align="center")

So, it will swap **element 4** with **element 3** (as the correct index of **element 4** is **index 3**).

![Image showing swap operation of element 4 with the element 3](https://cdn.hashnode.com/res/hashnode/image/upload/v1767719951745/21ba9cfb-0ad1-4f60-99cd-d63c09119e65.png align="center")

Now, it will check again: is **element 3** at its correct index? No, it isn't. The correct index of **3** is **index 2**.

![Image showing array with position of the control variable at index 0 and the element's correct index selected](https://cdn.hashnode.com/res/hashnode/image/upload/v1767882786056/c4718d64-3713-48d7-a952-f8f6f2b6d93e.png align="center")

So, **element 3** will be swapped with **element 1**.

![Image showing swap operation between element at index 0 and 2](https://cdn.hashnode.com/res/hashnode/image/upload/v1767882888825/456e889b-4ed5-4989-8aee-a2204b817dea.png align="center")

Now, the algorithm checks once again: is **element 1** at its correct index? Yes, it is!  
So, the algorithm will move to the next index and once again check if that element is at its correct index.

![Image showing next position of control variable in the array](https://cdn.hashnode.com/res/hashnode/image/upload/v1767883502749/3941b3a9-f6e2-474f-b6d2-7d2d19248331.png align="center")

Is **element 2** at its correct index? Yes, it is. The algorithm continues this process until it reaches the end of the array.

<div data-node-type="callout">
<div data-node-type="callout-emoji">💡</div>
<div data-node-type="callout-text">You might have already realized that the <strong>correct index</strong> for an element is its <strong>value - 1</strong>, if the range of numbers in the array is 1 to N.</div>
</div>

## Space Complexity

As this algorithm is an in-place sorting algorithm, it does not require any auxiliary space. So, its space complexity is **O(1)**.

## Time Complexity

We have two scenarios here: the **worst case** and the **best case**.

### Worst Case

The worst case happens when every number is in the wrong place in an array with a known range (say, 1 to N). The sample array used above, `[5, 4, 1, 3, 2]`, is an example of the worst case. Let's calculate how many times the algorithm performed checks.

In the example array, total 4 swaps and 5 checks were made. After all swaps were performed at the first index, the element at that index was checked once again. Therefore, there were a total of 5 checks.

In general, **N - 1 swaps** and **N checks** would be made. As in each swap, 1 check is performed. So, there would be a total of \\(2N-1\\) checks made.

Therefore, the worst-case time complexity of cyclic sort algorithm is **O(N)**.

### Best Case

The best case happens when the array is sorted in the desired order. In that case, the algorithm checks each element once and does not perform any swaps. Therefore, the best-case complexity is **O(N)**.

## Example Code

```java
import java.util.Arrays;

public class Main {
    public static void main(String[] args) {
        int[] arr = {2, 3, 5, 1, 4};
        sort(arr);
        System.out.println(Arrays.toString(arr));
    }

    static void sort(int[] arr) {
        int i = 0;
        while (i < arr.length) {
            // Assuming range of array is 1 to N
            int correctIndex = arr[i] - 1;
            if (arr[i] != arr[correctIndex]) {
                swap(arr, i, correctIndex);
            } else {
                i++;
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

Cyclic sort is a highly efficient algorithm for sorting arrays with elements in a known range, such as from 1 to N. It operates in-place, requiring no additional space, which makes it space-efficient with a complexity of **O(1)**. The algorithm's time complexity is **O(N)** in both the best and worst cases, making it a reliable choice for sorting tasks where the range of numbers is predetermined. By understanding the mechanics of cyclic sort, you can effectively apply it to relevant sorting problems, optimizing performance and resource usage.

⭐ Check out the [**DSA**](https://github.com/SaptarshiSarkar12/DSA) GitHub repo for more code examples.