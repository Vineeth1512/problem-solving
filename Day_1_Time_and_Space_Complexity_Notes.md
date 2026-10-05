# 🧠 DSA Problem-Solving --- Day 1

## Time Complexity & Space Complexity

> **Goal:** Learn how to measure the growth of an algorithm instead of
> memorizing solutions.

------------------------------------------------------------------------

## 📌 Day 1 Learning Map

``` text
Algorithm
   ↓
Input Size (n)
   ↓
Time Complexity
   ↓
Big O
   ├── O(1)
   ├── O(log n)
   ├── O(n)
   └── O(n²)
   ↓
Space Complexity
   ↓
Analyze Code
   ↓
Think Like a Problem Solver
```

------------------------------------------------------------------------

# 1. What Is an Algorithm?

### Definition

An **algorithm** is a step-by-step procedure used to solve a problem.

### 🌍 Real-Life Analogy

Think about making tea:

1.  Boil water
2.  Add tea powder
3.  Add milk
4.  Add sugar
5.  Boil
6.  Serve

That sequence is like an algorithm.

### 💻 Programming Example

``` javascript
function findMax(arr) {
    let max = arr[0];

    for (let i = 1; i < arr.length; i++) {
        if (arr[i] > max) {
            max = arr[i];
        }
    }

    return max;
}
```

The algorithm is:

1.  Assume the first element is maximum.
2.  Compare every remaining element.
3.  Update `max` when a larger value is found.
4.  Return the maximum.

### 🧠 Remember This

> **Recipe for food = Algorithm for a program.**

------------------------------------------------------------------------

# 2. What Is Input Size `n`?

### Definition

`n` represents the **size of the input**.

For an array:

``` javascript
const arr = [10, 20, 30, 40, 50];
```

``` text
n = arr.length
n = 5
```

If the array contains 1,000 elements:

``` text
n = 1000
```

### 🌍 Real-Life Analogy

Imagine a supermarket cashier.

-   5 customers → small workload
-   100 customers → larger workload
-   10,000 customers → huge workload

The number of customers is the **input size**.

### 🧠 Remember This

> **`n` = How much input the algorithm has to deal with.**

------------------------------------------------------------------------

# 3. What Is Time Complexity?

### Definition

**Time Complexity describes how the amount of work performed by an
algorithm grows as the input size `n` grows.**

It does **not** simply mean the exact number of seconds a program takes.

We are interested in the **growth of work**.

### 🌍 Real-Life Analogy

Imagine searching for a book.

If there are:

``` text
10 books → small amount of work
1,000 books → more work
1,000,000 books → much more work
```

We want to know:

> **How does the work grow when the number of books grows?**

That's the idea behind Time Complexity.

------------------------------------------------------------------------

# 4. Why Do We Need Big O?

Suppose two algorithms solve the same problem.

### Algorithm A

``` text
n operations
```

### Algorithm B

``` text
n² operations
```

For:

``` text
n = 10
```

``` text
A → 10
B → 100
```

For:

``` text
n = 1,000
```

``` text
A → 1,000
B → 1,000,000
```

For:

``` text
n = 1,000,000
```

``` text
A → 1,000,000
B → 1,000,000,000,000
```

The difference becomes enormous as `n` grows.

### 🧠 Big O helps us answer:

> **How efficiently does this algorithm scale?**

------------------------------------------------------------------------

# 5. Big O Notation

Common complexities:

``` text
O(1)
O(log n)
O(n)
O(n log n)
O(n²)
O(2ⁿ)
O(n!)
```

For Day 1, focus deeply on:

``` text
O(1)
O(log n)
O(n)
O(n²)
```

------------------------------------------------------------------------

# 6. O(1) --- Constant Time

### Definition

`O(1)` means the amount of work stays approximately constant regardless
of input size.

### 💻 JavaScript

``` javascript
function getFirst(arr) {
    return arr[0];
}
```

Whether:

``` text
n = 5
n = 100
n = 1,000,000
```

we still access one element.

Therefore:

``` text
Time = O(1)
```

### 🌍 Real-Life Analogy

Imagine a building with 1 million rooms.

Someone says:

> "Go directly to room #500."

You don't inspect every room.

You directly access room #500.

### 💻 Java

``` java
static int getFirst(int[] arr) {
    return arr[0];
}
```

``` text
Time = O(1)
Space = O(1)
```

### 🧠 Remember This

> **Direct access → O(1)**

------------------------------------------------------------------------

# 7. O(n) --- Linear Time

### 💻 JavaScript

``` javascript
function printNumbers(arr) {
    for (let i = 0; i < arr.length; i++) {
        console.log(arr[i]);
    }
}
```

If:

``` text
n = 5      → 5 iterations
n = 100    → 100 iterations
n = 1000   → 1000 iterations
```

Therefore:

``` text
Time = O(n)
```

### Why?

The algorithm processes every element once.

``` text
n elements
↓
1 complete pass
↓
n operations
↓
O(n)
```

### 🌍 Real-Life Analogy

A teacher takes attendance for every student.

-   30 students → 30 checks
-   100 students → 100 checks
-   1,000 students → 1,000 checks

### 💻 Java

``` java
static void printNumbers(int[] arr) {
    for (int i = 0; i < arr.length; i++) {
        System.out.println(arr[i]);
    }
}
```

``` text
Time = O(n)
Space = O(1)
```

### 🧠 Remember This

> **One complete pass through `n` elements → O(n).**

------------------------------------------------------------------------

# 8. O(n²) --- Quadratic Time

### 💻 JavaScript

``` javascript
function printPairs(arr) {
    for (let i = 0; i < arr.length; i++) {
        for (let j = 0; j < arr.length; j++) {
            console.log(arr[i], arr[j]);
        }
    }
}
```

Outer loop:

``` text
n times
```

For every outer iteration, inner loop:

``` text
n times
```

Total:

``` text
n × n = n²
```

Therefore:

``` text
Time = O(n²)
```

### 🌍 Real-Life Analogy

Imagine every student in a classroom has to interact with every other
student.

If there are `n` students:

``` text
n × n
```

interactions can occur.

### 💻 Java

``` java
static void printPairs(int[] arr) {
    for (int i = 0; i < arr.length; i++) {
        for (int j = 0; j < arr.length; j++) {
            System.out.println(arr[i] + " " + arr[j]);
        }
    }
}
```

``` text
Time = O(n²)
Space = O(1)
```

### 🧠 Remember This

> **Nested independent work → often O(n²).**

------------------------------------------------------------------------

# 9. O(log n) --- Logarithmic Time

### Definition

`O(log n)` usually occurs when the problem size is repeatedly reduced by
a constant factor, commonly by half.

### 🌍 Real-Life Analogy --- Dictionary Search

Imagine a dictionary with 1,000 pages.

Instead of starting at page 1:

``` text
1000
↓
500
↓
250
↓
125
↓
62
↓
31
↓
...
↓
1
```

Each step eliminates a large portion of the remaining search space.

That's logarithmic behavior.

------------------------------------------------------------------------

# 10. Why Is It `log n`?

Suppose:

``` text
n = 16
```

Repeatedly divide by 2:

``` text
16 → 8 → 4 → 2 → 1
```

Number of divisions:

``` text
4
```

Because:

``` text
log₂(16) = 4
```

For:

``` text
n = 32
```

``` text
32 → 16 → 8 → 4 → 2 → 1
```

That's 5 divisions:

``` text
log₂(32) = 5
```

### 🧠 Remember This

> **Repeatedly cutting the problem by a constant factor → O(log n).**

------------------------------------------------------------------------

# 11. Logarithmic Loop Example

### JavaScript

``` javascript
function example(n) {
    while (n > 1) {
        n = Math.floor(n / 2);
    }
}
```

For:

``` text
n = 16
```

Execution:

``` text
16 → 8 → 4 → 2 → 1
```

Therefore:

``` text
Time = O(log n)
Space = O(1)
```

### Java

``` java
static void example(int n) {
    while (n > 1) {
        n = n / 2;
    }
}
```

``` text
Time = O(log n)
Space = O(1)
```

------------------------------------------------------------------------

# 12. Multiplying by 2 Is Also O(log n)

Consider:

``` javascript
let i = 1;

while (i < n) {
    i = i * 2;
}
```

The values are:

``` text
1 → 2 → 4 → 8 → 16 → 32 → ...
```

The value grows exponentially.

If:

``` text
n = 8
```

then:

``` text
1 → 2 → 4 → 8
```

The loop body executes 3 times.

Therefore:

``` text
Time = O(log n)
```

### Important Pattern

These are usually logarithmic:

``` javascript
i = i * 2;
i = i * 3;
i = Math.floor(i / 2);
i = Math.floor(i / 3);
```

The important idea is:

> **The loop variable changes by a constant factor.**

------------------------------------------------------------------------

# 13. O(log n) Is NOT the Same as O(n/2)

A common mistake:

``` text
n = 1,000,000
```

An O(log n) algorithm does **not** mean:

``` text
500,000 iterations
```

Instead, it may take only around:

``` text
log₂(1,000,000) ≈ 20
```

iterations.

### 🧠 Remember This

> **O(log n) means the number of steps grows very slowly.**

------------------------------------------------------------------------

# 14. Comparing Complexity

For:

``` text
n = 1,000
```

Approximate work:

  Complexity     Approximate Work
  ------------ ------------------
  O(1)                          1
  O(log n)                   \~10
  O(n)                      1,000
  O(n²)                 1,000,000

For:

``` text
n = 1,000,000
```

  Complexity      Approximate Work
  ------------ -------------------
  O(1)                           1
  O(log n)                    \~20
  O(n)                   1,000,000
  O(n²)          1,000,000,000,000

### Key Lesson

> **As input grows, the growth rate matters more than the current input
> size.**

------------------------------------------------------------------------

# 15. Space Complexity

### Definition

**Space Complexity describes how the extra memory used by an algorithm
grows as the input size grows.**

### 🌍 Real-Life Analogy

Imagine going on a trip.

Your clothes are already your input.

If you need an additional bag to store things you collect, that
additional bag represents **extra memory**.

------------------------------------------------------------------------

# 16. O(1) Space

``` javascript
function sum(a, b) {
    let result = a + b;
    return result;
}
```

We only use a fixed number of variables.

Therefore:

``` text
Space = O(1)
```

Even if the input becomes huge, the number of extra variables doesn't
grow with `n`.

------------------------------------------------------------------------

# 17. O(n) Space

``` javascript
function copyArray(arr) {
    const result = [];

    for (let i = 0; i < arr.length; i++) {
        result.push(arr[i]);
    }

    return result;
}
```

If:

``` text
n = 10
```

we create about 10 additional elements.

If:

``` text
n = 1000
```

we create about 1000 additional elements.

Therefore:

``` text
Space = O(n)
```

### Java

``` java
static int[] copyArray(int[] arr) {
    int[] result = new int[arr.length];

    for (int i = 0; i < arr.length; i++) {
        result[i] = arr[i];
    }

    return result;
}
```

``` text
Space = O(n)
```

------------------------------------------------------------------------

# 18. Auxiliary Space

When interviewers ask for **auxiliary space**, they usually mean the
extra memory used by the algorithm apart from the input.

Example:

``` javascript
function findMax(arr) {
    let max = arr[0];

    for (let i = 1; i < arr.length; i++) {
        if (arr[i] > max) {
            max = arr[i];
        }
    }

    return max;
}
```

We only use a few variables:

``` text
max
i
```

No extra array is created.

Therefore:

``` text
Auxiliary Space = O(1)
```

### 🧠 Remember This

> **If extra memory does not grow with `n` → O(1) auxiliary space.**

------------------------------------------------------------------------

# 19. Best Case vs Worst Case

### Best Case

The input causes the algorithm to perform the **minimum amount of
work**.

### Worst Case

The input causes the algorithm to perform the **maximum amount of
work**.

------------------------------------------------------------------------

# 20. Example --- Linear Search

``` javascript
function findValue(arr, target) {
    for (let i = 0; i < arr.length; i++) {
        if (arr[i] === target) {
            return i;
        }
    }

    return -1;
}
```

### Best Case

Target is first:

``` text
[target, ...]
   ↑
found immediately
```

``` text
Best Time = O(1)
```

### Worst Case

Target is last:

``` text
[..., target]
```

or target doesn't exist.

We may check every element:

``` text
Worst Time = O(n)
```

### Space

``` text
Space = O(1)
```

### 🧠 Key Question

> **Can the algorithm stop early?**

If yes, the best case may be smaller.

------------------------------------------------------------------------

# 21. Important Example --- Find Maximum

``` javascript
function findMax(arr) {
    let max = arr[0];

    for (let i = 1; i < arr.length; i++) {
        if (arr[i] > max) {
            max = arr[i];
        }
    }

    return max;
}
```

A common mistake is to say:

``` text
Best = O(1)
```

because the first element might already be the maximum.

But the algorithm still has to inspect every element to prove it is the
maximum.

Therefore:

``` text
Best Time  = O(n)
Worst Time = O(n)
Space      = O(1)
```

### 🧠 Remember This

> **Best case is NOT automatically O(1). Ask whether the algorithm can
> stop early.**

### 🌍 Memory Hook

Finding the tallest person in a room:

Even if the first person looks very tall, you must check everyone before
declaring them the tallest.

------------------------------------------------------------------------

# 22. Complexity Calculation Rules

## Rule 1 --- Direct Access

``` javascript
arr[0]
```

``` text
O(1)
```

------------------------------------------------------------------------

## Rule 2 --- One Complete Pass

``` javascript
for (let i = 0; i < n; i++) {
    // work
}
```

``` text
O(n)
```

------------------------------------------------------------------------

## Rule 3 --- Nested Loops

``` javascript
for (let i = 0; i < n; i++) {
    for (let j = 0; j < n; j++) {
        // work
    }
}
```

``` text
n × n
= n²
= O(n²)
```

------------------------------------------------------------------------

## Rule 4 --- Sequential Loops

``` javascript
for (...) {
    // n
}

for (...) {
    // n
}
```

Total:

``` text
n + n
= 2n
= O(n)
```

### Remember:

> **Sequential → Add**

------------------------------------------------------------------------

## Rule 5 --- Nested Work

``` text
n × n
```

### Remember:

> **Nested → Multiply**

------------------------------------------------------------------------

## Rule 6 --- Different Growth Rates

``` text
O(n + n²)
```

Keep the fastest-growing term:

``` text
O(n²)
```

Similarly:

``` text
O(n + log n)
→ O(n)

O(n² + n + 1)
→ O(n²)
```

### 🧠 Remember This

> **When terms are added, keep the fastest-growing term.**

------------------------------------------------------------------------

# 23. Constants in Big O

We ignore constant multipliers.

``` text
O(2n) → O(n)

O(5n) → O(n)

O(100n) → O(n)
```

But:

``` text
O(n²)
```

is fundamentally different from:

``` text
O(n)
```

### Why?

Because constants don't change the growth category.

------------------------------------------------------------------------

# 24. Common Mistakes

### ❌ Mistake 1

> "Input has n elements, so every operation runs n times."

Wrong.

Example:

``` javascript
arr[0]
```

is:

``` text
O(1)
```

even if the array contains 1 million elements.

------------------------------------------------------------------------

### ❌ Mistake 2

> "One loop always means O(n)."

Not necessarily.

Look at how the loop variable changes.

``` javascript
i++
```

usually gives:

``` text
O(n)
```

But:

``` javascript
i *= 2
```

gives:

``` text
O(log n)
```

------------------------------------------------------------------------

### ❌ Mistake 3

> "Two loops always means O(n²)."

Wrong.

Sequential loops:

``` text
n + n
= O(n)
```

Nested loops:

``` text
n × n
= O(n²)
```

------------------------------------------------------------------------

### ❌ Mistake 4

> "Best case is always O(1)."

Wrong.

`findMax()` has:

``` text
Best = O(n)
Worst = O(n)
```

because it cannot stop early.

------------------------------------------------------------------------

### ❌ Mistake 5

> "O(log n) means n/2 operations."

Wrong.

`O(log n)` means the number of steps grows logarithmically, usually
because the problem is repeatedly reduced or the loop variable changes
by a constant factor.

------------------------------------------------------------------------

# 25. Interview Answers

## Q: What is Time Complexity?

### Natural Answer

> "Time complexity describes how the amount of work performed by an
> algorithm grows as the input size increases."

------------------------------------------------------------------------

## Q: What is Space Complexity?

> "Space complexity describes how the extra memory used by an algorithm
> grows as the input size increases."

------------------------------------------------------------------------

## Q: What is the complexity of a single loop?

> "If the loop processes all `n` elements once, its time complexity is
> O(n)."

------------------------------------------------------------------------

## Q: Why is a nested loop O(n²)?

> "The outer loop runs n times, and for each outer iteration the inner
> loop also runs n times. So the total work is n multiplied by n, which
> gives O(n²)."

------------------------------------------------------------------------

## Q: Why is Binary Search O(log n)?

> "Binary Search reduces the search space by roughly half after every
> comparison. Therefore the number of steps grows logarithmically with
> the input size."

------------------------------------------------------------------------

## Q: Can you optimize this?

Don't immediately start coding.

Think:

``` text
What is causing the expensive work?
        ↓
Repeated searching?
Nested loops?
Duplicate calculations?
Sorting?
Large extra memory?
        ↓
Can a different data structure or pattern reduce it?
```

------------------------------------------------------------------------

# 26. The Complexity Decision Process

Whenever you see code, follow this process:

``` text
STEP 1
↓
What is n?

STEP 2
↓
What work is performed?

STEP 3
↓
How many times does that work execute?

STEP 4
↓
Is the work sequential or nested?

STEP 5
↓
Does the loop variable change by a constant factor?

STEP 6
↓
Are there multiple complexity terms?

STEP 7
↓
Keep the fastest-growing term.

STEP 8
↓
Check extra memory.

STEP 9
↓
Give Time + Space Complexity.
```

------------------------------------------------------------------------

# 27. Quick Complexity Cheat Sheet

  Pattern                    Typical Complexity
  ------------------------ --------------------
  Direct array access                      O(1)
  Simple calculation                       O(1)
  One complete loop                        O(n)
  Two sequential loops                     O(n)
  Three sequential loops                   O(n)
  Nested two loops                        O(n²)
  Nested three loops                      O(n³)
  Repeated divide by 2                 O(log n)
  Repeated multiply by 2               O(log n)
  Binary Search                        O(log n)
  Extra array of size n              O(n) space
  Few variables                      O(1) space

> ⚠️ These are pattern-recognition rules, not universal laws. Always
> inspect how the code actually progresses.

------------------------------------------------------------------------

# 28. The Four Core Complexities

Think of them visually:

``` text
O(1)
──────
Doesn't grow


O(log n)
──────
Grows very slowly


O(n)
──────
Grows directly with input


O(n²)
──────
Grows extremely quickly
```

### Growth Order

From generally better to worse as `n` becomes very large:

``` text
O(1)
  ↓
O(log n)
  ↓
O(n)
  ↓
O(n log n)
  ↓
O(n²)
  ↓
O(2ⁿ)
  ↓
O(n!)
```

------------------------------------------------------------------------

# 29. 🧠 Day 1 Remember This

## Core Rules

> **Direct access → O(1)**

> **One complete pass → O(n)**

> **Repeatedly divide/multiply by a constant → O(log n)**

> **Nested n × n work → O(n²)**

> **Sequential work → Add**

> **Nested work → Multiply**

> **Different growth rates → Keep the fastest-growing term**

> **Best case = minimum work**

> **Worst case = maximum work**

> **Extra memory that grows with n → O(n)**

> **Fixed amount of extra memory → O(1)**

------------------------------------------------------------------------

# 30. 🌍 Final Memory Analogy

Imagine searching for a book.

### O(1)

You know the exact shelf.

``` text
Go directly → Done
```

### O(n)

You check every book one by one.

``` text
Book 1
Book 2
Book 3
...
Book n
```

### O(log n)

You use a dictionary-like strategy and repeatedly eliminate half.

``` text
n
↓
n/2
↓
n/4
↓
n/8
↓
...
```

### O(n²)

You compare every book with every other book.

``` text
Book 1 → compare with n books
Book 2 → compare with n books
...
Book n → compare with n books
```

``` text
n × n = n²
```

------------------------------------------------------------------------

# 🎯 Day 1 Practice Status

You practiced:

-   [x] O(1)
-   [x] O(n)
-   [x] O(n²)
-   [x] O(log n)
-   [x] Best case
-   [x] Worst case
-   [x] Space complexity
-   [x] Sequential loops
-   [x] Nested loops
-   [x] Complexity simplification
-   [x] Logarithmic loops

## Next Topic

### 🚀 Binary Search

We'll learn:

``` text
What is Binary Search?
        ↓
Why does it require sorted data?
        ↓
Real-life analogy
        ↓
Manual problem solving
        ↓
JavaScript implementation
        ↓
Java implementation
        ↓
Internal execution
        ↓
O(log n) analysis
        ↓
Practice problems
```

> **Goal:** Don't memorize Binary Search. Learn how to recognize when a
> problem can eliminate half of its search space.

------------------------------------------------------------------------

## ⭐ Final Day 1 Rule

> **Don't ask only "What is the Big O?"**
>
> Ask:
>
> **"How does the amount of work change when `n` becomes bigger?"**

That question is the foundation of algorithmic thinking.
