---
title: "What is Recursion? A Comprehensive Overview"
seoTitle: "Understanding Recursion: A Complete Guide"
seoDescription: "Master recursion: Fibonacci numbers, binary search, base conditions, recurrence relations, and complexity insights"
datePublished: Fri Jan 16 2026 05:16:30 GMT+0000 (Coordinated Universal Time)
cuid: cmkgfel14000502l12ldtb1xx
slug: what-is-recursion-a-comprehensive-overview
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1768540536899/a41b5590-3871-401c-8c69-a3bdc4e73836.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1768540543378/57d68a76-d40a-4815-9b08-f2effa51f671.png
tags: java, recursion, dsa, dsainjava

---

## A Problem

Let’s start with a problem: **I need to print first 10 natural numbers**.

There are several ways to solve this problem. But let's say we need to **solve it using functions without using loops or calling a function more than once**. The simplest way is to call 10 functions, each printing one of the numbers from 1 to 10.

```java
public class Problem {
    public static void main(String[] args) {
        print1();
    }

    public static void print1(){
        System.out.println(1);
        print2();
    }

    public static void print2(){
        System.out.println(2);
        print3();
    }

    public static void print3(){
        System.out.println(3);
        print4();
    }

    public static void print4(){
        System.out.println(4);
        print5();
    }

    public static void print5(){
        System.out.println(5);
        print6();
    }

    public static void print6(){
        System.out.println(6);
        print7();
    }

    public static void print7(){
        System.out.println(7);
        print8();
    }

    public static void print8(){
        System.out.println(8);
        print9();
    }

    public static void print9(){
        System.out.println(9);
        print10();
    }

    public static void print10(){
        System.out.println(10);
    }
}
```

Let’s try to understand how the function calls are happening internally.

I’ll try to debug that code by putting the debug pointer at the line calling `print1()` function.

![Image showing position of debug pointer](https://cdn.hashnode.com/res/hashnode/image/upload/v1768405323181/c860ccc6-b740-4493-a63a-8cef5d036ddc.png align="center")

When you start the debug window in IntelliJ IDEA, you can see the function calls in the call stack on the left side of the window.

![Image showing initial call of print1 function](https://cdn.hashnode.com/res/hashnode/image/upload/v1768405445321/9b778251-d5f1-4385-ba00-30c4302d1428.png align="center")

When `print1()` function is called, it appears on top of the `main()` function in the call stack.

![Image of call stack after print1 function is called](https://cdn.hashnode.com/res/hashnode/image/upload/v1768405563329/88890ca7-b84c-413e-a72c-2084ee274955.png align="center")

After `print1()` function displays **1** in the output, it calls `print2()` function and so on. Finally, `print10()` function gets called.

![Image of call stack showing that print10 function was called](https://cdn.hashnode.com/res/hashnode/image/upload/v1768405590103/2c5d717a-ac41-41ec-9d2c-0e63a7b51bc0.png align="center")

After printing **10**, the `print10()` call finishes execution, so its stack frame is removed (popped) from the call stack and control returns to the caller (which is `print9()` function).

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1768405862445/58bfa284-fab2-4171-9111-37ed0d3f02c4.png align="center")

Finally, each of the stack frames are removed until the main function completes its execution.

However, the code is messy!

![Messy Messy Messy GIFs | Tenor](https://media1.tenor.com/m/UhfGKQ2LD_wAAAAC/frosty-the-snowman-smh.gif align="center")

## The Idea of Recursion

If we look closely, each of the 10 functions we defined earlier has the same structure. They each print a number and then call the next function in order. If we were given the task to print natural numbers upto a million, defining a million functions would be terrific.

To summarize, we solved the bigger problem of printing the first 10 natural numbers by breaking it down into 10 smaller parts. Each function handles the task of printing one number at a time.

Hence, we can think of recursion as **breaking down a problem into sub-problems until it becomes trivial**.

If we look at the code again, each function calls the next one until the last function (`print10()`). So, we can rewrite the function to print the current number and then call itself with the next number in sequence until it reaches number 10.

```java
public class Problem {
    public static void main(String[] args) {
        print(10);
    }

    public static void print(int n) {
        // Base Condition: Exit when n is 0 or negative
        if (n <= 0) {
            return;
        }
        // Recursive call/relation: Calls itself by passing the next smaller element
        print(n - 1);
        // Return Flow / Work after recursion
        System.out.println(n);
    }
}
```

This is called as **recursion,** and the `print()` function is called as **recursive function**. There are three parts of any recursive function:

1. **Base Condition**: The condition where the recursion stops
    
2. **Recurrence Relation**: This relation defines how the problem is reduces to smaller sub-problems.
    
3. **Return Relationship/Flow**: This defines how the result of the smaller sub-problem is used when the function call returns.
    

## Recursive Tree

To better understand how the function call happens, we need to know about **recursive tree** which is a visual representation of the recursive calls. The below image shows a recursive tree for our program.

![Recursive tree](https://cdn.hashnode.com/res/hashnode/image/upload/v1768409024359/7cde64a4-34f3-41dd-a9be-e80c7e36b15e.png align="center")

## Finding a Fibonacci number using recursion

The **nth** Fibonacci number is equal to the sum of the **(n-1)th** and **(n-2)th** Fibonacci numbers. So, the problem of finding the **nth** Fibonacci number can be broken down to smaller problems. Hence, this problem *can be solved using* ***recursion***.

We got the following recurrence relation:

$$Fibo(n) = Fibo(n-1) + Fibo(n-2)$$

So, the recursive tree for **Fibo(4)** will be:

![Recursive tree of finding 4th Fibonacci number](https://cdn.hashnode.com/res/hashnode/image/upload/v1768433270479/0723787d-dabd-4c7f-bf1b-848a8055cd20.png align="center")

We know that the first 2 numbers of the Fibonacci series are 0 and 1. So, value of **Fibo(1)** and **Fibo(0)** are 1 and 0 respectively. Hence, the function must stop calling itself again when the value of n becomes 1 or 0. Therefore, this becomes the **base condition**.

Here’s the code for finding nth Fibonacci number using recursion:

```java
public class Problem {
    public static void main(String[] args) {
        System.out.println(fibo(5));
    }

    public static int fibo(int n) {
        // Base Condition
        if (n < 2) {
            return n;
        }
        // Recurrence Relation and Return Relationship
        return fibo(n-1) + fibo(n-2);
    }
}
```

Using the recursive tree, we can better understand the order of function calls. First, **Fibo(4)** calls **Fibo(3)** (since **fibo(n-1)** is written first), which then calls **Fibo(2)**. Next, **Fibo(2)** calls **Fibo(1)**. Since no further function call is made, **Fibo(1)** returns its value as 1.

![Recursive tree showing the first function call execution and its return value](https://cdn.hashnode.com/res/hashnode/image/upload/v1768435387223/3ca30085-8d29-42e6-921a-1696256f22f2.png align="center")

To calculate the value of **Fibo(2)**, we need the value of **Fibo(0)**, so **Fibo(0)** is called and returns 0. Then, **Fibo(1)** is called because it is needed to compute the value of **Fibo(3)**.

![Recursive tree showing the completion of the execution of the left part of the recursive tree](https://cdn.hashnode.com/res/hashnode/image/upload/v1768435526770/43b8c805-67c9-4cf4-983d-9523223bf94f.png align="center")

The value of **Fibo(4)** depends on **Fibo(2)**, which in turn depends on **Fibo(1)** and **Fibo(0)**, leading to those function calls.

![Image of the complete recursive tree showing each return values](https://cdn.hashnode.com/res/hashnode/image/upload/v1768435656028/6cd41e2a-7854-4ace-99be-99b730ff9a88.png align="center")

Finally, **Fibo(4)** computes the sum and returns the value as **3**.

## Tail Recursion

The most important type of recursive function is the **tail recursive function**. This is a recursive function where the last operation is the recursive call itself. If we rewrite the initial recursive program that prints natural numbers from 1 to 10 using the code below, we can make it a tail recursive function.

```java
public class Problem {
    public static void main(String[] args) {
        print(1, 10);
    }

    public static void print(int current, int n) {
        // Base Condition: Exit when current exceeds n
        if (current > n) {
            return;
        }
        // Print the current value
        System.out.println(current);
        // Tail recursive call
        print(current + 1, n);
    }
}
```

The recursive Fibonacci function is not a tail recursive function because, after making the **Fibo(n-1)** and **Fibo(n-2)** recursive calls, it adds their returned values. Therefore, the last operation is **not the recursive call itself**.

## Binary Search using recursion

In the [binary search algorithm](https://saptarshisarkar.hashnode.dev/everything-you-need-to-know-about-binary-search), we always check if the **middle element** is equal to the **target element**. If the check fails, the search space is cut in half each time. This means the task of checking for equality is done in smaller, reduced sections of the original array. Hence, the binary search algorithm can be implemented using recursion.

The binary search algorithm stops when the equality check is met, so the recursion must end when this condition is satisfied. Therefore, the **equality check** becomes the **base condition**.

As the search space of the array is halved each time, the **start** and **end** values of the search space are needed in every recursive function call. Therefore, the **start** and **end** pointer values will be included in the function parameters. The index of the middle element (`mid`) depends on the **start** and **end** index values, so it doesn't need to be passed to future recursive calls. Therefore, `mid` will be calculated within the function.

Based on whether the middle element is greater or less than the target element, the function will make its next recursive call with updated start or end pointer values. The result of this call will be the position of the target element if it exists in the array, or an indication that the element is not present.

```java
public class Problem {
    public static void main(String[] args) {
        int[] arr = {12, 34, 54, 72, 88, 99, 101, 123, 145, 167};
        int target = 101;
        int result = binarySearch(arr, target, 0, arr.length - 1);
        System.out.println("Element found at index: " + result);
    }

    public static int binarySearch(int[] arr, int target, int start, int end) {
        if (start > end) {
            return -1;
        }
        int mid = start + (end - start) / 2; // to avoid integer overflow
        if (arr[mid] == target) {
            return mid;
        } else if (arr[mid] < target) {
            return binarySearch(arr, target, mid + 1, end);
        } else {
            return binarySearch(arr, target, start, mid - 1);
        }
    }
}
```

We perform two tasks:

1. Comparing the middle element with the target element. This takes a constant amount of time. So, time complexity of comparison is **O(1)**.
    
2. Searching for the target element in half of the previous search space.
    

So, the recurrence relation would be:

$$F(N) = O(1) + F(\frac {N}{2})$$

where **F** is the binary search function and **N** is the size of the array.

The relation above means that when a target number is provided, a comparison is first made. Then, the number is searched for in half of the previous search space of the array.

## Space Complexity

As in recursion, we are calling the function **n times** and each function call goes in the call stack, so space complexity of a recursive algorithm is not constant.

## Conclusion

Recursion is a powerful programming concept that allows complex problems to be broken down into simpler, more manageable sub-problems. By understanding the key components of recursion—base condition, recurrence relation, and return flow—developers can effectively implement recursive solutions for various problems, such as calculating Fibonacci numbers or performing binary searches. While recursion can lead to elegant and concise code, it is important to consider its space complexity due to the call stack usage. Mastering recursion can greatly enhance problem-solving skills and lead to more efficient algorithms.

⭐ Check out the [**DSA**](https://github.com/SaptarshiSarkar12/DSA) GitHub repo for more code examples.