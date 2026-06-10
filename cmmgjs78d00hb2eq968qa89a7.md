---
title: "Key Math Concepts in Data Structures and Algorithms"
seoTitle: "Mathematical Foundations of Data Structures and Algorithms"
seoDescription: "Discover the mathematical foundations of data structures and algorithms—number systems, bitwise logic, primes, modular arithmetic, and more."
datePublished: 2026-03-07T16:38:28.770Z
cuid: cmmgjs78d00hb2eq968qa89a7
slug: maths-for-dsa
cover: https://cdn.hashnode.com/uploads/covers/628869289490454c4d8475de/b66154cd-e2aa-457b-915e-e87806b23c42.png
tags: algorithms, java, maths, mathematics, dsa, number-theory

---

At the core of data structures and algorithms are fundamental mathematical principles that guide their design and implementation. This article explores key math concepts essential for mastering data structures and algorithms, helping developers write optimized and effective code.

## Number Systems

A **number system** is a structured way of representing numbers using specific symbols and rules. Different number systems are based on different **base values** (also called the *radix*).

We are most familiar with the **decimal number system**, which is used in everyday life. It uses ten digits (**0 through 9**) to represent all numbers. Because it uses ten distinct digits, its base is **10**.

Computers, however, operate using only two digits: **0** and **1**. Therefore, they use the **binary number system**, which has a base of **2**. All data inside a computer is ultimately stored and processed in binary form.

The **octal number system** uses eight digits (**0 to 7**) so its base is **8**. It is used as a more compact way to represent binary numbers, since each octal digit corresponds to a group of **three binary digits (bits)**. Octal is still used in certain areas of computing, such as **file permissions in Unix and Linux systems**.

The **hexadecimal number system** uses sixteen symbols: the digits **0–9** and the letters **A–F**. Because it has sixteen symbols, its base is **16**. Each hexadecimal digit corresponds to a group of **four binary digits**, making it a convenient way to represent memory addresses, machine code, and other low-level data in computers.

> The **octal number system** has a base of 8, which means it uses eight symbols: 0 to 7.  
> Since **8 = 2³**, each octal digit can represent exactly **three binary digits (bits)**. Same goes for hexadecimal number system.

You can learn how to convert between these number systems from [this detailed article](https://www.geeksforgeeks.org/digital-logic/number-system-and-base-conversions/).

Now, let’s talk about the binary number system. We are familiar with representing positive numbers using unsigned binary. But how do we represent negative numbers? For this, we use the **two’s complement method**, which is the standard way to represent signed binary numbers.

### Two's complement method

Negative of any decimal number is mathematically found by subtracting that number from 0. The same applies to the binary number system. In the signed binary number system, the **most significant bit** (the leftmost bit) indicates the sign of the number.

> See the image below if you are not familiar with the most and least significant bits in the binary representation of a number:
> 
> ![Image of a binary number whose MSB and LSB are indicated](https://cdn.hashnode.com/res/hashnode/image/upload/v1771301336808/840ccc91-fd56-4047-9041-e1c5f1ed2bab.png align="center")

Let’s take the example of decimal 7 whose binary representation is 0111. Its binary number system is stored in 4 bits. Zero can be represented as 0000 (in 4 bits). In 4-bit representation, if a fifth bit is present in the leftmost position, it is discarded due to lack of space. So, we can represent zero as **1***0000* (the bit 1 will be discarded). Now, **10000** can be written as the sum of **1111** and **1**. We can then proceed as follows:

![Image showing calculation for finding the negative of an unsigned binary number](https://cdn.hashnode.com/res/hashnode/image/upload/v1771291657535/9ea48090-ea1d-4a5b-9ff1-fb0d1c51638f.png align="center")

Essentially, **the negative of a binary number will be its complement added to 1**. This method is called as the [two’s complement method](https://en.wikipedia.org/wiki/Two%27s_complement).

## Bitwise Operators

In the decimal number system, we use arithmetic operators like +, -, \*, and / to perform mathematical operations. In computing, numbers are represented in binary, and in addition to arithmetic operators, we also use bitwise operators like &, |, ^, ~, >>, and << to manipulate individual bits. Let’s discuss each of these operators.

### AND Operator (&)

This operator performs bit-by-bit AND operation on two values. This means that for each bit in the operands, the resulting bit is set to 1 only if both corresponding bits in the operands are 1; otherwise, it is set to 0.

**Observation:**

The AND operation of any number with 1 gives the **least significant bit** (LSB) of that number.  
*Example*: 5 & 1 results in 1 because 101 & 001 gives its LSB, which is 1.

### OR Operator (|)

This operator performs a bitwise OR operation between two operands, setting each resulting bit to 1 if at least one of the corresponding bits in the operands is 1; otherwise, it is set to 0.

### XOR Operator (^)

XOR stands for **exclusive OR**. This operator performs a bitwise comparison between two operands, setting each resulting bit to 1 if the corresponding bits in the operands are different; otherwise, it is set to 0.

**Observations:**

1.  The XOR operation on any number with 1, results in a number where the **least significant bit** (LSB) is flipped.  
    *Example*: 3 ^ 1 results in 2 because 11 ^ 01 changes the LSB to 0 in this case.
    
2.  The XOR operation on any number with 0 results in the same number.  
    *Example*: 4 ^ 0 results in 4 because 100 ^ 000 gives 100, which is 4.
    
3.  The XOR operation on any number with itself results in 0 because there are no differing bits.  
    *Example*: 5 ^ 5 results in 0 because 101 ^ 101 gives 0 as there are no bits that differ.
    

### Complement Operator (~)

The complement operator gives the bitwise inverse of a number, flipping each bit from 0 to 1 and from 1 to 0.

### Left Shift Operator (<<)

The left shift operator is a bitwise operator that shifts the bits of a number to the left by a specified number of positions.

*Example*: 5 << 1 gives 10 because shifting the bits of 5 (which is 101 in binary) one position to the left results in 1010, which is 10 in decimal.

If we shift twice (5 << 2), we would get 20 because shifting the bits of 5 (which is 101 in binary) two positions to the left results in 10100, which is 20 in decimal.

Therefore, each left shift operation effectively multiplies the number by 2 for each position shifted. In general, if the number is shifted k times, it is multiplied by 2^k.

### Right Shift Operator (>>)

The right shift operator is a bitwise operator that shifts the bits of a number to the right by a specified number of positions.

*Example*: 8 >> 1 gives 4 because shifting the bits of 8 (which is 1000 in binary) one position to the right results in 0100, which is 4 in decimal.

If we shift twice (8 >> 2), we would get 2 because shifting the bits of 8 (which is 1000 in binary) two positions to the right results in 0010, which is 2 in decimal.

Therefore, each right shift operation effectively divides the number by 2 for each position shifted. In general, if the number is shifted k times, it is divided by 2^k.

## Core Number Theory

### Prime Number

A prime number is a natural number greater than 1 with exactly two positive divisors: 1 and itself. To determine if a number is prime, we typically check divisibility from **2** up to **n−1** since it is always divisible by 1 and itself.

```java
int n = 24;
boolean isPrime = true;
for (int i = 2; i < n; i++) {
    if (n % i == 0) {
        isPrime = false;
        break;
    }
}
if (isPrime) {
    System.out.println("Prime");
} else {
    System.out.println("Not prime");
}
```

The above algorithm makes a maximum of **n - 2** (2 to n-1) checks. So, its time complexity is **O(N)**. Let's see if we can optimise it.

If we closely examine the factors of any number, they appear in pairs (one smaller and one larger). Mathematically, we can say that for every divisor d > √n (*like d = 6*), there exists a corresponding divisor \\(\frac {n} {d} < \sqrt n\\) (*like 4*). Therefore, checking beyond √n is redundant.

![Image showing all pairs of factors of 24](https://cloudmate-test.s3.us-east-1.amazonaws.com/uploads/covers/628869289490454c4d8475de/ae7349e0-0bcf-4d9b-9578-24ffed628d95.png align="center")

If we look into the above possible pairs of factors of 24, we can see that we're checking divisibility of each pair twice. It is sufficient to check divisibility only up to **√n** since √24 ≈ 4.89, checking up to 4 is enough. Hence, we can reduce the number of computations from the order of **N** to **√N**.

```java
int n = 24;
boolean isPrime = true;
for (int i = 2; i * i <= n; i++) {
    if (n % i == 0) {
        isPrime = false;
        break;
    }
}
if (isPrime) {
    System.out.println("Prime");
} else {
    System.out.println("Not prime");
}
```

The time complexity of this algorithm is now **O(√N)**.

### Prime Numbers in Range

Let's say we need to find prime numbers between two certain numbers. The simplest idea would be to check if **each of the numbers** between them is **prime** or not.

```java
public class Main {
    public static void main(String[] args) {
        int n = 50;
        displayAllPrimes(n);
    }
    
    public static void displayAllPrimes(int n){
        for (int i = 2; i <= n; i++) {
            if (isPrime(i)) {
                System.out.print(i + " ");
            }
        }
    }
    
    public static boolean isPrime(int n){
        if (n <= 1) return false;
        for (int i = 2; i * i <= n; i++) {
            if (n % i == 0) return false;
        }
        return true;
    }
}
```

In the above program, the `isPrime()` method takes **O(√N)** to check whether a certain number is prime. The `displayAllPrimes()` method calls the `isPrime()` method approximately **N times**. So, the time complexity of the entire algorithm is **O(N√N)**.

If we carefully observe the numbers we're checking for prime, we'll notice that there are a number of redundant checks. For example, if we already know that 2 is a prime number then its multiples won't be prime.

![Image showing multiples of the prime number 2](https://cdn.hashnode.com/uploads/covers/628869289490454c4d8475de/f43c11cb-83c2-478f-b55b-3871011ccbd8.png align="center")

Similarly for the rest of the numbers, the below image shows the multiples of smaller prime numbers we've checked earlier.

![Image showing all the multiples of each prime numbers marked](https://cdn.hashnode.com/uploads/covers/628869289490454c4d8475de/1b7fa69e-cee6-478c-9a2d-72a868e04a6d.png align="center")

The unmarked numbers turn out to be the **prime numbers** we're finding in that **range of 2 to 50**. This is known as the **Sieve of Eratosthenes**.

```java
public class Sieve {
    public static void main(String[] args) {
        int n = 50;
        boolean[] isComposites = new boolean[n+1]; // size is n+1 to include n 
        sieve(n, isComposites);
    }

    public static void sieve(int n, boolean[] isComposite){
        for (int i = 2; i * i <= n; i++) {
            if (!isComposite[i]) {
                for (int j = 2 * i; j <= n; j += i) {
                    isComposite[j] = true;
                }
            }
        }

        for (int i = 2; i <= n; i++) {
            if (!isComposite[i]) {
                System.out.print(i + " ");
            }
        }
    }
}
```

In the program above, we check for multiples up to **√N** because large numbers can be factored using smaller numbers' multiples.

The number of times the inner loop (the loop responsible for marking the composite numbers) runs for each prime number **P** is \\(\frac {N} {P}\\). Therefore, total number of times the inner loop runs will be:

![Image showing calculation of time complexity of Sieve of Eratosthenes](https://cdn.hashnode.com/uploads/covers/628869289490454c4d8475de/3754f281-3094-4dc8-87e1-3ca516c17243.png align="center")

Hence, the time complexity of this algorithm is **O(N loglog(N))**.

### Newton Raphson Method

The Newton Raphson method is an iterative method of finding better approximations to the roots of a real-valued function. The best linear approximation to any differential function near the point \\(x = x_i\\) will be its tangent with the equation:

$$y = f'(x_i)(x - x_i) + f(x_i)$$

where \\(x_i\\) is the ith iterative approximation of root

The root of the tangent equation will be the next iterative approximation \\(x_{i+1}\\) when it intercepts the x-axis (y = 0).

![Image showing derivation of equation for i+1 th approximation ](https://cdn.hashnode.com/uploads/covers/628869289490454c4d8475de/4a8807a9-24dc-421e-807a-48137df931df.png align="center")

Now, if we want to find the square root of any number (say **n**), we can take f(x) = x² - n. The root of that equation will give us the closest approximation of **√n**.

![Image showing the derivation of the equation for finding the i+1 th iterative approximation for the square root of n](https://cdn.hashnode.com/uploads/covers/628869289490454c4d8475de/28ed9672-f7a3-4498-96c2-71be6864d2ec.png align="center")

> You can view [this animated image from Wikipedia](https://upload.wikimedia.org/wikipedia/commons/e/e0/NewtonIteration_Ani.gif), which visually demonstrates all the iteration of approximated roots of f(x).

Let's try to write a program for finding the approximate square root of any number.

```java
public class NewtonRaphsonSqrt {
    public static void main(String[] args) {
        System.out.println(sqrt(43));
    }

    public static double sqrt(double n) {
        double x = n;
        double root;
        while (true) {
            root = 0.5 * (x + (n/x));

            if (Math.abs(root - x) < 0.5) { // Error threshold, can be adjusted for more precision
                break;
            }
            x = root;
        }
        return root;
    }
}
```

Reducing the error threshold, currently set at 0.5, will result in a more accurate approximation of the square root.

### Modular Arithmetic

It is a system of arithmetic operations for integers where the numbers "*wrap around*" when exceeding a certain number called as the **modulus**. For a given integer m ≥ 1, it is called a modulus if the difference of two integers **a** and **b** (*a - b*) is an integer multiple of **m** i.e. a - b = k\*m (where k is an integer). The integers **a** and **b** are said to be congruent modulo m and is mathematically denoted by **a ≡ b (mod m)**.

> The parentheses mean that (mod *m*) applies to the entire equation, not just to the right-hand side (here, *b*). In particular, **(*a* mod *m*) = (*b* mod *m*)** is equivalent to ***a* ≡ *b* (mod *m*)**, and this explains why "=" is often used instead of "≡" in this context.
> 
> The congruence relation is written as **a = b + k\*m**.
> 
> Source: [Wikipedia](https://en.wikipedia.org/wiki/Modular_arithmetic#Congruence)

In programming, we don’t write congruences directly. Instead, we use the `%` operator, which computes the remainder. The `%` operator is the practical realization of the congruence relation. For example: 𝑎 ≡ 𝑏 (mod m) ⇔ (a % m) == (b % m) in code.

The range of (**a % m**) is always in the range (**\[0, m-1\]**) when (m > 0). This ensures the remainder is non-negative, which is crucial for consistent modular arithmetic in programming.

**Properties:**

1.  **Addition Property**  
    When adding two numbers, their remainders modulo (m) add up, but if the sum exceeds (m), subtracting (m) (i.e., taking modulo again) brings it back within the valid range.
    
    $$(a + b) \bmod m = ((a \bmod m) + (b \bmod m)) \bmod m$$
    
2.  **Subtraction Property**  
    Subtraction can lead to negative results, so adding (m) before taking modulo ensures the result stays within (**\[0, m-1\]**).
    
    $$(a - b) \bmod m = ((a \bmod m) - (b \bmod m) + m) \bmod m$$
    
3.  **Multiplication Property**  
    Multiplying the remainders and then taking modulo keeps the product within the modular system, preserving equivalence.
    
    $$(a \times b) \bmod m = ((a \bmod m) \times (b \bmod m)) \bmod m$$
    
4.  **Division Property**  
    Division is not straightforward in modular arithmetic. For division by (b) modulo (m) to be valid, (b) must have a modular inverse modulo (m), which exists only if gcd(b, m) = 1.
    
    $$\frac{a}{b} \bmod m = a \times b^{-1} \bmod m = ((a \bmod m) \times (b^{-1} \bmod m)) \bmod m$$
    
    Modular multiplicative inverse of an integer b is the solution (which exists only when b and m are coprime) of the below equation:
    
    $$ax\equiv 1 {\pmod {m}}$$
    

### **Bézout's Identity**

It is a theorem which related two arbitrary integers with their greatest common divisor (GCD). Mathematically,

![Image showing bezout's identity relation](https://cdn.hashnode.com/uploads/covers/628869289490454c4d8475de/cbd13049-1d9e-49c5-95be-ae193c53ec55.png align="center")

where, x and y are integers.

If `gcd(a, b) = d`, then every integer linear combination `ax + by` is a multiple of d.

For example, if a = 3 and b = 16, then 3\*(-5) + 16\*1 = 1 = gcd(3, 16).  
Let's take another example: a = 8 and b = 18. Then, 8\*(-2) + 18\*1 = 2 = gcd(8, 18).

The coefficients x and y can be found using the Extended Euclidean algorithm and the gcd can be calculated using the Euclidean algorithm.

### Euclidean Algorithm

The Euclidean Algorithm is one of the oldest and most efficient methods to compute the greatest common divisor (GCD) of two integers. Since Bézout’s identity relies on the GCD, understanding this algorithm is essential. It's based on the principle that if

Effectively, a is reduced by multiples of b until only the remainder is left. Therefore, gcd(a, b) = gcd(b, a % b).

Let’s compute **gcd⁡(514, 106)** using the Euclidean Algorithm.

We start by dividing the larger number by the smaller one and continue replacing the pair with (b, a % b) until the remainder becomes zero:

1.  514 = 106\*4 + 90  
    → gcd⁡(514, 106) = gcd⁡(106, 90)
    
2.  106 = 90\*1 + 16  
    → gcd⁡(106, 90) = gcd⁡(90, 16)
    
3.  90 = 16\*5 + 10  
    → gcd⁡(90, 16) = gcd⁡(16, 10)
    
4.  16 = 10\*1 + 6  
    → gcd⁡(16,10) = gcd⁡(10, 6)
    
5.  10 = 6\*1 + 4  
    → gcd⁡(10, 6) = gcd⁡(6, 4)
    
6.  6 = 4\*1 + 2  
    → gcd⁡(6, 4) = gcd⁡(4, 2)
    
7.  4 = 2\*2 + 0  
    → gcd⁡(4, 2) = 2
    

Therefore, gcd(514, 106) = 2.

```java
public static int gcd(int a, int b) {
    if (a == 0) {
        return b;
    }
    return gcd(b % a, a);
}
```

We can also calculate the LCM of two numbers using their GCD with the formula: $$\\text{LCM}(a, b) = \\frac{|a \\times b|}{\\text{GCD}(a, b)}$$

```java
public static int lcm(int a, int b) {
    return a * b / gcd(a, b);
}
```

### Extended Euclidean Algorithm

This algorithm is an extension of the Euclidean Algorithm which computes the coefficients of the Bézout's identity. We start with the gcd of the two numbers and eventually represent that as a linear combination of those two numbers.

For example, we have found **gcd(514, 106) = 2**. We start with the last non-zero remainder step: 6 = 4 + 2 ⇒ 2 = 6 - 4.  
Then, from previous steps, we can write **6 = 16 - 10** and **4 = 10 - 6**. We'll back-substitute them in the above equation.  
∴ 2 = (16-10) - (10 - 6) = 16 - 2\*10 + 6 = 16 - 2\*10 + (16 - 10) = 2\*16 - 3\*10  
We can write 10 as **90 - 16\*5** (from Euclidean Algorithm's steps).  
∴ 2 = 2\*16 - 3\*(90 - 16\*5) = 17\*16 - 3\*90  
We can write 16 as **106 - 90** (from **2nd step**)  
∴ 2 = 17\*(106 - 90) - 3\*90 = 17\*106 - 20\*90  
We can further write 90 as **514 - 106\*4**.  
∴ 2 = 17\*106 - 20\*(514 - 4\*106) = (-20)\*514 + 97\*106

Hence, (-20)\*514 + 97\*106 = 2 = gcd(514, 106). So, the coefficients (**Bézout's coefficients**) of Bézout's identity would be **\-20** and **97**.

We can utilise the recursion stack to keep track of the steps performed in Euclidean Algorithm. Below is the code for this algorithm:

```java
static int gcdExtended(int a, int b, int[] xy) {
    if (a == 0) {
        xy[0] = 0; // x
        xy[1] = 1; // y
        return b;
    }

    int[] temp = new int[2];
    int gcd = gcdExtended(b % a, a, temp);

    // Update x and y using results of recursion
    xy[0] = temp[1] - (b / a) * temp[0];
    xy[1] = temp[0];

    return gcd;
}
```

## Conclusion

In this article, we explored fundamental mathematical concepts that are crucial for understanding and implementing data structures and algorithms. We delved into number systems, including binary, octal, and hexadecimal, and discussed how computers represent numbers using the two's complement method for signed integers. We also covered bitwise operators and their applications in manipulating individual bits of data.

⭐ Check out the [DSA](https://github.com/SaptarshiSarkar12/DSA) GitHub repo for more code examples.