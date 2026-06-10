---
title: "Demystifying Time and Space Complexity for Beginners"
seoTitle: "Understanding Time and Space Complexity"
seoDescription: "Learn the basics of time and space complexity analysis for efficient algorithm comparison, including Big O, Big Theta, and Big Omega notations"
datePublished: 2026-02-04T01:06:39.844Z
cuid: cml7bugys000102jr9y4i393d
slug: demystifying-time-and-space-complexity-for-beginners
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1770167140160/14c4e861-8029-4ead-8528-53e7bfa33982.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1770167093936/9c413874-9d1a-448e-8820-8f6dc9c7b100.png
tags: algorithms, recursion, time-complexity, dsa, callstack, algorithm-analysis, dsainjava, space-complexity, complexity-analysis

---

Imagine you've just created an algorithm, and it works lightning-fast on your brand-new computer. You're thrilled with the results and can't wait to share your success, so you ask your friend to give it a try. However, when your friend runs the same algorithm on his older computer, it doesn't perform as well and turns out to be quite slow. This unexpected result leaves you both puzzled and curious about what might be causing the difference in speed.

## Why We Need Complexity Analysis?

As we saw in the problem mentioned earlier, the same algorithm can take different amounts of time to run depending on the machine it's on. In real-world situations, we often need to compare multiple algorithms to choose the best and fastest one. Hardware differences can lead to incorrect conclusions. That's why complexity analysis was introduced — to standardize the comparison between algorithms by ignoring hardware differences.

The concept of complexity measures how performance changes as the input size increases. We always test with large input sizes to reflect real-world scenarios where we might be dealing with vast amounts of data.

## What is Time Complexity?

Time complexity measures how the **running time** increases as the input size grows. It focuses on the **number of operations** an algorithm performs, not the actual time it takes.

## What is Space Complexity?

**Space complexity** is a measure of the amount of memory an algorithm uses as the size of the input increases, including both the **input space** and the **auxiliary space** (the extra space taken).

I want to point out that in **recursion**, multiple recursive calls use a certain amount of stack space, which is also considered **auxiliary space**.

## Why do we need Asymptotic Notations?

In practical situations, we often need to compare algorithms to find the most efficient one. Remembering the exact function of time (or space) taken as the input size **n** changes is challenging. For instance, the time it takes for an algorithm to finish can be expressed as \\(5n^2 + 3n + 2\\). This is complex and not practical for comparison. So, we use asymptotic notations to simplify these expressions and focus on the most significant factors that affect performance (or in other words, approximate them to a simpler function), making it easier to compare different algorithms.

## Big-O Notation

Big-O notation is a mathematical concept used to describe an upper bound on the growth rate of an algorithm’s time or space complexity. Formally, it means that for sufficiently large input size *n*, the complexity function 𝑓(*n*) does not grow faster than a constant multiple of another function 𝑔(*n*).

Mathematically,

$$f(n) = O(g(n))$$

if and only if the below condition is satisfied.

$$0 \le f(n) \le c.g(n), \ n \ge n_0$$

where, c is a constant and \\(n_0\\) is the threshold value above which the condition is satisfied for all large numbers.

For example, let’s say \\(f(n) = 16n^2 + 2n + 3\\).

We need to find a suitable g(n) that will satisfy the condition. So, we can proceed as follows:

![Image showing how function g is obtained by comparing each part of function f](https://cdn.hashnode.com/res/hashnode/image/upload/v1769146705092/07b8e9bc-2c2c-46dd-b1a0-19ce6d647712.png align="center")

Comparing this with the given condition, we get **c = 21** and **g(n) = n²**.

If we put n as 1, we get f(1) as 21 and 21n² as 21. So, the equality holds and 1 can be a potential threshold value. We will still check for large values of n like 5 in which case the inequality holds. So, the value of \\(n_0\\) turns out to be 1.  
Therefore, \\(f(n) = O(n^2) \ \forall \ n \ge 1\\).

If we look at the same problem again, we can argue as follows:

![Image showing another possible equation of function g](https://cdn.hashnode.com/res/hashnode/image/upload/v1769147016669/ef6aa4e1-c77c-40cb-8259-27978ede59ae.png align="center")

This gives us g(n) as n³. We could choose other higher powers of n, but 21n² is the most accurate approximation of the original function. Therefore, we should always choose the **smallest upper bound** to get the closest curve fit.

## Big-Omega Notation

Big-Omega notation is a mathematical way to express the asymptotic lower bound of a function (time or space complexity). It provides a formal way to describe the minimum time an algorithm will take to complete, regardless of the input size.

Mathematically,

$$f(n) = \Omega(g(n))$$

if and only if the below condition is satisfied.

$$f(n) \ge c.g(n), \ n \ge n_0$$

where, c is a constant and \\(n_0\\) is the threshold value above which the condition is satisfied for all large numbers.

For example, let’s say \\(f(n) = 16n^4+13n+12\\).

We can easily conclude that \\(f(n) >= 16n^4\\). If we put \\(n = 1\\), then \\(f(1)\\) is 41 which is ≥ 16. Therefore, we can say \\(f(n) = \Omega (n^4)\\) for all *n* ≥ 1.

Similarly, as we have seen in the case of Big-O, f(n) is ≥ n³, ≥ n², ≥ n, etc. But we should \\(n^4\\) as g(n) because \\(16n^4\\) is the tightest polynomial that consistently under-approximates f(n) without overshooting.

## Big-Theta Notation

Big-Theta notation is a mathematical way to express **both** the **asymptotic lower** and the **upper bounds** of a **tightly bounded function** (time or space complexity).

Mathematically,

$$f(n) = \Theta (g(n))$$

if and only if the below condition is satisfied.

$$0 \le c_1.g(n) \le f(n) \le c_2.g(n), \ n \ge n_0$$

where, \\(c_1\\) and \\(c_2\\) are constants and \\(n_0\\) is the threshold value above which the condition is satisfied for all large numbers.

For example, let’s say \\(f(n) = 16n^2 + 12\\).

We can proceed as follows:

$$16n^2 \le 16n^2 + 12 \le 16 n^2 + 12n^2 \\ \implies 16n^2 \le 16n^2 + 12 \le 28 n^2$$

Comparing this with the aforementioned inequality, we get **g(n)** = **n²**.

If we set **n** to 1, the inequality holds true. Checking with the next number, 2, the inequality still holds. Therefore, \\(n_0\\) must be 1.

Hence, we can asymptotically say \\(f(n) = \Theta (n^2)\\) for all n ≥ 1.

## Best, Average and Worst Case

There are three scenarios to consider when analyzing algorithms: the **best** case, the **average** case, and the **worst** case. Of these, the worst case provides the most accurate estimate of the time or space an algorithm will require in the most demanding situation, often reflecting real-world scenarios. Hence, the worst case is the most usually preferred.

## How to calculate Time Complexity for iterative programs?

Let’s understand the procedure to calculate time complexity through examples.

### Example 0

The below code is for printing **first N natural numbers**.

```java
for (int i = 1; i <= n; i++) {
    System.out.println(i);
}
```

In the code snippet above, the loop runs **N times** (from 1 to N) and each time we are **printing a number** (which takes a constant amount of time). Therefore, we are performing **constant** amount of work **N times**. So, the growth rate will be linear. Hence, this algorithm has a time complexity of **O(N)**.

### Example 1

```java
int i = 1;
int s = 1;
while (s <= n) {
    i++;
    s = s + i;
    System.out.println(s);
}
```

We should analyse the values of **i** and **s** to check how many times the print statement (a constant time work) is executed.

![Table illustrating the values of i and s at each iteration of the while loop](https://cdn.hashnode.com/res/hashnode/image/upload/v1769744785517/cba7a43e-8983-4fe6-896d-85733b2013b1.png align="center")

In the above table, we can observe that:

* 3 = 1 + 2 = \\(\frac {2*(2+1)} {2}\\)
    
* 6 = 1 + 2 + 3 = \\(\frac {3*(3+1)} {2}\\)
    
* 10 = 1 + 2 + 3 + 4 = \\(\frac {4*(4+1)} {2}\\)
    

So, asymptotically, since constants don't change the growth rate of **s**, it grows on the order of **k²**. Therefore, we take the values of **i** and **s** as **k** and **k²** respectively for the kth iteration.

The while loop will stop when **s &gt; n**, which means **k² &gt; n**. Therefore, **k** must be equal to **√n**. As a result, the constant time task of printing the value of **s** will happen **√n** times. Thus, the time complexity of this code snippet is **O(√n)**.

### Example 2

```java
for (int i = 1; i <= n; i++) {
    for (int j = 1; j <= i*i; j++) {
        for (int k = 1; k <= n/2; k++) {
            System.out.println(k);
        }
    }
}
```

We need to analyze how often the constant task of printing the value of **k** happens. To do this, we'll create a table showing how many times the loops for i, j, and k run.

![Table illustrating the number of times the i, j and k loop runs based on values of i till it becomes equal to n](https://cdn.hashnode.com/res/hashnode/image/upload/v1769746535756/2adfdd64-2553-4e59-b1df-bd612ab5498e.png align="center")

The outermost for loop (**loop i**) runs until i equals n. Therefore, the total time the innermost loop runs will be the sum of the times it executes for each combination of i and j values.

![Image showing calculation of the total number of times the innermost loop is run over all possible combinations of values of i and j](https://cdn.hashnode.com/res/hashnode/image/upload/v1769747029110/3c7eb501-ee9c-4d16-9458-f235058ea188.png align="center")

Therefore, the constant work is performed in the order of \\(n^4\\). Hence, the time complexity for this code snippet is \\(O(n^4)\\).

## Types of Recurrence Relations

There are two types of recurrence relations:

1. Linear Recurrence Relation: These express the next term as a linear combination of previous terms (e.g., Fibonacci sequence).
    
2. Divide and Conquer Relation: These arise in recursive algorithms where a problem is divided into subproblems, solved recursively, and combined (e.g., Merge Sort, Binary Search).
    

## How to calculate Time Complexity for recursive programs?

There are three ways to calculate time complexity given the recurrence relation:

1. Back-Substitution Method
    
2. Recursive Tree Method
    
3. Akra–Bazzi Method
    

Let’s learn these methods in detail.

### Back-Substitution Method

Let’s take the following linear recurrence relation as an example:

![Image showing a linear recurrence relation in the form of a picewise function](https://cdn.hashnode.com/res/hashnode/image/upload/v1769749192862/c62ac85d-02c0-4653-bfe2-0d928be29085.png align="center")

We'll start by finding **T(n-1)** and **T(n-2)**, and then substitute them back into the equation. Next, we'll generalize the equation for the kth substitution and try to substitute the constant given for the base condition (i.e., when n = 0).

![Image showing equations of linear recurrence for n-1 and n-2 input size](https://cdn.hashnode.com/res/hashnode/image/upload/v1769750161909/177079a2-10ea-45f1-bd97-614e194c32bb.png align="center")

Therefore, we can write **T(n)** as:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1769750773373/52bdf84a-0d32-4a45-8b08-41bbfe4edd89.png align="center")

Now, **T(n-k)** will be equal to **T(0)** when **n-k = 0**, i.e. when k = n.

\\(\therefore T(n) = T(0) + n = 1 + n\\)

Hence, time complexity of this **T(n)** function would be **O(N)**.

### Recursive Tree Method

Let’s take the following **linear recurrence relation** as an example:

![Image of a linear recurrence relation in the form of a picewise function](https://cdn.hashnode.com/res/hashnode/image/upload/v1769751409983/fd33ebe5-9a78-46bc-9a14-6f93a108f59e.png align="center")

We'll try to visualize the recursive calls and the constant values at each call as a recursive tree.

![Image of the recursive tree](https://cdn.hashnode.com/res/hashnode/image/upload/v1769754505825/39df642e-00d6-4e43-a3e5-e7ec494458f0.png align="center")

The total time taken for the complete recursive function will be the cumulative sum of work done at each level of recursion, with each level contributing an amount equal to its index (**n**). Therefore, total time = \\(1 + 2 + ... + (n-2) + (n-1) + n\\) = \\(\frac {n*(n+1)} {2}\\) which is a quadratic growth of time. Hence, time complexity will be **O(N²)**.

Let's take an example of a **divide-and-conquer recurrence relation** and try to solve it using this method.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1769838524956/59cdd64f-8238-44c7-9171-29ec21b067d2.png align="center")

We’ll again draw the recursive tree to visualise the recursive calls made.

![Recursive tree showing top 3 levels of recursive calls and the last level where no further recursive calls are made](https://cdn.hashnode.com/res/hashnode/image/upload/v1769839854906/e5b47255-51c9-4d10-9645-e309647ca447.png align="center")

To find the total time complexity, we simply look at the work done across the tree horizontally. At the top level, the work is ***n***. At the second level, we have two branches doing \\(n/2\\) work, which again sums to ***n***. Surprisingly, if you sum the work across any horizontal level of this tree, it always equals ***n***. Therefore, the total time is simply the work per level (**n**) multiplied by the number of levels (the height of the tree).

![Image showing recursive tree with calculation of work done per level](https://cdn.hashnode.com/res/hashnode/image/upload/v1769840493709/40ab2c61-8e44-482e-afd8-0b36e7eb96e1.png align="center")

To find the total number of levels, we'll assume the last level is the ***k***th level. At the ***i***th level, the input to the function is \\(\frac {n} {2^i}\\). So, at the last level, \\(T(\frac {n} {2^k}) = T(1)\\), which means \\(\frac {n} {2^k} = 1\\), leading to \\(k = log_2 n\\).

Hence, time complexity will be **O(n\*log n)**.

### Akra-Bazzi Method

[This method](https://en.wikipedia.org/wiki/Akra%E2%80%93Bazzi_method) is a generalization of the [Master Theorem](https://en.wikipedia.org/wiki/Master_theorem_\(analysis_of_algorithms\)) for divide-and-conquer recurrences. Mathematically, if the function **T(x)** can be represented as

![Image of the form of function T(x)](https://cdn.hashnode.com/res/hashnode/image/upload/v1769991294653/40ec892d-3d90-4e97-b173-d8bc8390cdb5.png align="center")

where:

* `p` must be such that \\(\sum_{i=1}^{k} a_i b_i^p = 1\\)
    
* \\(a_i > 0\\) and \\(0 < b_i < 1\\) for all *i*
    

Then,

![Image showing function T(x) would be a theta of some function](https://cdn.hashnode.com/res/hashnode/image/upload/v1769991534071/702b5c5d-f69a-4ad8-9ebf-9ad526edbe01.png align="center")

For example, let's consider the following recurrence relation, which has been solved using other methods:

![Image of a divide-and-conquer recurrence relation](https://cdn.hashnode.com/res/hashnode/image/upload/v1769838524956/59cdd64f-8238-44c7-9171-29ec21b067d2.png align="center")

Comparing with the standard equation, we get:

* \\(a_1 = 2\\)
    
* \\(b_1 = \frac {1} {2}\\)
    
* \\(g(n) = n\\)
    

We can proceed as follows, to find the value of *p*.

![Image showing equation for finding the value of p](https://cdn.hashnode.com/res/hashnode/image/upload/v1769992330021/41cad522-52cf-4f3e-9204-70620469aee3.png align="center")

Therefore, time complexity of T(n) would be:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1769992668535/99875386-0815-4c1a-85de-dd3ee07d309b.png align="center")

## How to calculate Space Complexity?

### For Iterative Programs

Let's look at the two code snippets below as **examples 1** and **2**:

```java
// Example 1
int[] arr = {54, 26, 35, 85, 90};
int max = arr[0];
for (int i = 1; i < arr.length; i++) {
    if (arr[i] > max) {
        max = arr[i];
    }
}
System.out.println("The maximum value in the array is: " + max);
```

```java
// Example 2
int[] arr = {54, 26, 35, 85, 90};
int[] revArr = new int[arr.length];
for (int i = 0; i < arr.length; i++) {
    revArr[i] = arr[arr.length - 1 - i];
}
for (int num : revArr) {
    System.out.println(num);
}
```

In the first example, we're finding the maximum element in the array. If we closely analyze the algorithm, it uses only a constant number of extra variables (`max` and the loop counter `i`), **regardless of the size of the input array**. Since the extra space needed **does not increase** with the input size, the space complexity is **O(1)**.

In the second example, the algorithm reverses the array by creating a new array `revArr` whose size **depends** on the input size `N`. Apart from this array, only a **constant** number of extra variables (such as loop counters) are used. Since the auxiliary space required **grows linearly** with the input size, the space complexity is **O(N)**.

We can modify the algorithm to reverse the array **in place** by performing swap operations between elements from the beginning and end of the array. This approach eliminates the need for an additional array. The algorithm uses only a constant number of extra variables (such as `temp` and the loop counter), regardless of the input size. Therefore, the auxiliary space complexity of this approach is **O(1)**.

```java
// Modified Example 2
int[] arr = {54, 26, 35, 85, 90};
for (int i = 0; i < arr.length / 2; i++) {
    // Swap to reverse the array in-place
    int temp = arr[i];
    arr[i] = arr[arr.length - 1 - i];
    arr[arr.length - 1 - i] = temp;
}
for (int num : arr) {
    System.out.println(num);
}
```

### For recursive programs

In recursive programs, each recursive function call is added to the call stack, creating a stack frame (or activation record) for each call.

> **Call Stack** is a data structure used in programming languages to manage the functions calls and their execution. It works on **LIFO (Last-in, First-out)** principle where the most recently called function is executed first and removed from the stack once completed.

Let’s look at the following recurrence relation, which we have already solved for time complexity:

![Image of a linear recurrence relation](https://cdn.hashnode.com/res/hashnode/image/upload/v1769838524956/59cdd64f-8238-44c7-9171-29ec21b067d2.png align="center")

We need to analyze the recursive calls (especially their order). So, we’ll take a look at its recursive tree:

![Recursive tree showing top 3 levels of recursive calls and the last level where no further recursive calls are made](https://cdn.hashnode.com/res/hashnode/image/upload/v1769839854906/e5b47255-51c9-4d10-9645-e309647ca447.png align="center")

First, the leftmost branches are called, and after they execute, each of these function calls is removed from the call stack, starting from the bottom of the recursive tree. Then, the function calls in their respective right branches are executed. Here is an image of the flow of execution of the leftmost branches:

![Image of recursive tree showing the flow of execution](https://cdn.hashnode.com/res/hashnode/image/upload/v1770165141944/add6506e-767a-4cdf-b4da-a841e65d1a5c.png align="center")

This is how the **call stack** would appear until the T(1) function completes its execution:

![Image of call stack](https://cdn.hashnode.com/res/hashnode/image/upload/v1770166295404/7e54fbd5-9463-4670-bd34-efa7d13e8f7b.png align="center")

The total space used in the call stack for executing the leftmost branches is equal to the **height of the recursive tree** (which is also known as **maximum recursion depth**), which is **log n** as calculated before.  
This is the *maximum space* used in the complete execution of the program as for further calls (suppose from **T(n/2²)** to **second T(n/2³)**), the stack frames of the previous calls (the *series* of calls from the **first T(n/2³)** and **T(n/2³) itself**) are removed.

This is the complete view of the function calls:

![Image of the recursive tree showing the complete flow of execution](https://cdn.hashnode.com/res/hashnode/image/upload/v1770166072535/6cb20886-2d46-4bae-bbd8-b83cd3c74a3c.png align="center")

Hence, space complexity would be **O(log n)**.

## Conclusion

Understanding time and space complexity is crucial for evaluating and optimizing algorithms, especially as input sizes grow. By analyzing complexity, we can make informed decisions about which algorithms are most efficient, regardless of hardware differences. Asymptotic notations like Big-O, Big-Omega, and Big-Theta provide a standardized way to express these complexities, focusing on the most significant factors affecting performance.

Through examples, we've explored how to calculate time complexity for both iterative and recursive programs, as well as how to determine space complexity. Mastering these concepts allows developers to write more efficient code, ultimately leading to better performance in real-world applications.