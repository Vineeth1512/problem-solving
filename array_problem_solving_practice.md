# Array Problem-Solving Practice — JavaScript & Java

## What I Practiced

This document contains the array problems we practiced, with:
- Problem statement
- JavaScript solution
- Java solution
- Time and space complexity
- Key pattern / learning point
- Important edge cases

---

# 1. Sum of Array Elements

## Problem
Find the sum of all elements in an array.

### Example
```text
Input:  [10, 20, 30, 40]
Output: 100
```

## JavaScript

```javascript
function sum(arr) {
    let sum = 0;

    for (let i of arr) {
        sum += i;
    }

    return sum;
}

console.log(sum([10, 20, 30, 40]));
```

## Java

```java
public static int sum(int[] arr) {
    int sum = 0;

    for (int i : arr) {
        sum += i;
    }

    return sum;
}
```

## Complexity
- Time: O(n)
- Space: O(1)

## Pattern
**Accumulator pattern**

```text
Initialize → Traverse → Accumulate → Return
```

---

# 2. Find Maximum Element

## Problem
Find the largest element in an array.

### Example
```text
Input:  [10, 25, 7, 45, 18]
Output: 45
```

## JavaScript

```javascript
function findMax(arr) {
    let max = arr[0];

    for (let i of arr) {
        if (i > max) {
            max = i;
        }
    }

    return max;
}

console.log(findMax([10, 25, 7, 45, 18]));
```

## Java

```java
public static int findMax(int[] arr) {
    int max = arr[0];

    for (int i : arr) {
        if (i > max) {
            max = i;
        }
    }

    return max;
}
```

## Complexity
- Time: O(n)
- Space: O(1)

## Pattern
**Track the best value so far**

---

# 3. Count Positive, Negative and Zero

## Problem
Count how many positive numbers, negative numbers and zeros are present.

### Example
```text
Input:  [10, -5, 0, 20, -8, 0, 15, -2]

Positive: 3
Negative: 3
Zero:     2
```

## JavaScript

```javascript
function countNumbers(arr) {
    let positive = 0;
    let negative = 0;
    let zero = 0;

    for (let i of arr) {
        if (i === 0) {
            zero++;
        } else if (i > 0) {
            positive++;
        } else {
            negative++;
        }
    }

    return [positive, negative, zero];
}

console.log(countNumbers([10, -5, 0, 20, -8, 0, 15, -2]));
```

## Java

```java
public static int[] countNumbers(int[] arr) {
    int positive = 0;
    int negative = 0;
    int zero = 0;

    for (int i : arr) {
        if (i == 0) {
            zero++;
        } else if (i > 0) {
            positive++;
        } else {
            negative++;
        }
    }

    return new int[]{positive, negative, zero};
}
```

## Complexity
- Time: O(n)
- Space: O(1) extra space

## Pattern
**Classification / counting**

---

# 4. Find Second Largest Element

## Problem
Find the second largest element.

Assume there are at least two distinct values.

### Example
```text
Input:  [10, 25, 7, 45, 18, 32]
Output: 32
```

## JavaScript

```javascript
function findSecondLargest(arr) {
    let max = -Infinity;
    let secondMax = -Infinity;

    for (let i of arr) {
        if (i > max) {
            secondMax = max;
            max = i;
        } else if (i > secondMax) {
            secondMax = i;
        }
    }

    return secondMax;
}

console.log(findSecondLargest([10, 25, 7, 45, 18, 32]));
```

## Java

```java
public static int findSecondLargest(int[] arr) {
    int max = Integer.MIN_VALUE;
    int secondMax = Integer.MIN_VALUE;

    for (int i : arr) {
        if (i > max) {
            secondMax = max;
            max = i;
        } else if (i > secondMax) {
            secondMax = i;
        }
    }

    return secondMax;
}
```

## Complexity
- Time: O(n)
- Space: O(1)

## Pattern
**Two best values**

### Memory Hook
> New champion → old champion moves to second place.

---

# 5. Reverse an Array In-Place

## Problem
Reverse an array without creating another array.

### Example
```text
Input:  [10, 20, 30, 40, 50]
Output: [50, 40, 30, 20, 10]
```

## JavaScript

```javascript
function reverseArray(arr) {
    let left = 0;
    let right = arr.length - 1;

    while (left < right) {
        let temp = arr[left];
        arr[left] = arr[right];
        arr[right] = temp;

        left++;
        right--;
    }

    return arr;
}

console.log(reverseArray([10, 20, 30, 40, 50]));
```

## Java

```java
public static int[] reverseArray(int[] arr) {
    int left = 0;
    int right = arr.length - 1;

    while (left < right) {
        int temp = arr[left];
        arr[left] = arr[right];
        arr[right] = temp;

        left++;
        right--;
    }

    return arr;
}
```

## Complexity
- Time: O(n)
- Space: O(1)

## Pattern
**Two pointers — opposite ends**

---

# 6. Count Even Numbers

## Problem
Count the number of even elements.

### Example
```text
Input:  [10, 15, 22, 31, 40, 51, 60]
Output: 4
```

## JavaScript

```javascript
function countEven(arr) {
    let count = 0;

    for (let i of arr) {
        if (i % 2 === 0) {
            count++;
        }
    }

    return count;
}

console.log(countEven([10, 15, 22, 31, 40, 51, 60]));
```

## Java

```java
public static int countEven(int[] arr) {
    int count = 0;

    for (int i : arr) {
        if (i % 2 == 0) {
            count++;
        }
    }

    return count;
}
```

## Complexity
- Time: O(n)
- Space: O(1)

## Pattern
**Counting**

---

# 7. Check Whether Target Exists — Linear Search

## Problem
Return `true` if a target exists in the array, otherwise `false`.

### Example
```text
Input:  [10, 25, 7, 45, 18, 32], target = 10
Output: true
```

## JavaScript

```javascript
function contains(arr, target) {
    for (let i of arr) {
        if (target === i) {
            return true;
        }
    }

    return false;
}

console.log(contains([10, 25, 7, 45, 18, 32], 10));
```

## Java

```java
public static boolean contains(int[] arr, int target) {
    for (int i : arr) {
        if (target == i) {
            return true;
        }
    }

    return false;
}
```

## Complexity
- Best time: O(1)
- Worst time: O(n)
- Space: O(1)

## Pattern
**Linear search + early return**

---

# 8. Find Index of Target

## Problem
Return the index of the target. Return `-1` if it does not exist.

### Example
```text
Input:  [10, 25, 7, 45, 18, 32], target = 45
Output: 3
```

## JavaScript

```javascript
function findIndex(arr, target) {
    for (let i = 0; i < arr.length; i++) {
        if (arr[i] === target) {
            return i;
        }
    }

    return -1;
}

console.log(findIndex([10, 25, 7, 45, 18, 32], 45));
```

## Java

```java
public static int findIndex(int[] arr, int target) {
    for (int i = 0; i < arr.length; i++) {
        if (arr[i] == target) {
            return i;
        }
    }

    return -1;
}
```

## Complexity
- Best time: O(1)
- Worst time: O(n)
- Space: O(1)

---

# 9. Find First Occurrence

## Problem
Find the index of the first occurrence of a target.

### Example
```text
Input:  [10, 20, 30, 20, 40, 20], target = 20
Output: 1
```

## JavaScript

```javascript
function findFirstOccurrence(arr, target) {
    for (let i = 0; i < arr.length; i++) {
        if (arr[i] === target) {
            return i;
        }
    }

    return -1;
}

console.log(findFirstOccurrence([10, 20, 30, 20, 40, 20], 20));
```

## Java

```java
public static int findFirstOccurrence(int[] arr, int target) {
    for (int i = 0; i < arr.length; i++) {
        if (arr[i] == target) {
            return i;
        }
    }

    return -1;
}
```

## Complexity
- Time: O(n)
- Space: O(1)

## Pattern
**Return immediately when the first match is found.**

---

# 10. Find Last Occurrence

## Problem
Find the index of the last occurrence of a target.

### Example
```text
Input:  [10, 20, 30, 20, 40, 20], target = 20
Output: 5
```

## JavaScript

```javascript
function findLastOccurrence(arr, target) {
    let last = -1;

    for (let i = 0; i < arr.length; i++) {
        if (arr[i] === target) {
            last = i;
        }
    }

    return last;
}

console.log(findLastOccurrence([10, 20, 30, 20, 40, 20], 20));
```

## Java

```java
public static int findLastOccurrence(int[] arr, int target) {
    int last = -1;

    for (int i = 0; i < arr.length; i++) {
        if (arr[i] == target) {
            last = i;
        }
    }

    return last;
}
```

## Complexity
- Time: O(n)
- Space: O(1)

## Pattern
**Keep updating the answer; return after the loop.**

### Memory Hook

```text
First occurrence → return immediately
Last occurrence  → keep searching
```

---

# 11. Count Occurrences of a Target

## Problem
Count how many times a target appears.

### Example
```text
Input:  [10, 20, 30, 20, 40, 20], target = 20
Output: 3
```

## JavaScript

```javascript
function countOccurrences(arr, target) {
    let count = 0;

    for (let i of arr) {
        if (i === target) {
            count++;
        }
    }

    return count;
}

console.log(countOccurrences([10, 20, 30, 20, 40, 20], 20));
```

## Java

```java
public static int countOccurrences(int[] arr, int target) {
    int count = 0;

    for (int i : arr) {
        if (i == target) {
            count++;
        }
    }

    return count;
}
```

## Complexity
- Time: O(n)
- Space: O(1)

## Pattern
**Initialize counter → check condition → increment → return**

---

# 12. Check Whether All Elements Are Positive

## Problem
Return `true` only if every element is positive.

### Example
```text
[10, 20, 5, 30]     → true
[10, -5, 20, 30]    → false
```

## JavaScript

```javascript
function areAllPositive(arr) {
    for (let i of arr) {
        if (i <= 0) {
            return false;
        }
    }

    return true;
}

console.log(areAllPositive([10, 20, 5, 30]));
```

## Java

```java
public static boolean areAllPositive(int[] arr) {
    for (int i : arr) {
        if (i <= 0) {
            return false;
        }
    }

    return true;
}
```

## Complexity
- Worst time: O(n)
- Best time: O(1)
- Space: O(1)

## Pattern
**ALL condition**

### Memory Hook
> One failure is enough to return `false`.

---

# 13. Check Whether Array Is Sorted

## Problem
Check whether an array is sorted in ascending order.

Equal neighboring values are allowed.

### Examples
```text
[10, 20, 30, 40] → true
[10, 30, 20, 40] → false
[5, 5, 10, 20]   → true
```

## JavaScript

```javascript
function isSorted(arr) {
    for (let i = 1; i < arr.length; i++) {
        if (arr[i] < arr[i - 1]) {
            return false;
        }
    }

    return true;
}

console.log(isSorted([10, 20, 30, 40, 50]));
```

## Java

```java
public static boolean isSorted(int[] arr) {
    for (int i = 1; i < arr.length; i++) {
        if (arr[i] < arr[i - 1]) {
            return false;
        }
    }

    return true;
}
```

## Complexity
- Time: O(n)
- Space: O(1)

## Pattern
**Neighbor comparison**

### Memory Hook
> Compare `arr[i]` with `arr[i - 1]`.

---

# 14. Largest Absolute Difference Between Adjacent Elements

## Problem
Find the largest absolute difference between adjacent elements.

### Example
```text
Input:  [10, 15, 7, 20, 12]
Output: 13
```

Because:

```text
|10 - 15| = 5
|15 - 7|  = 8
|7 - 20|  = 13
|20 - 12| = 8
```

## JavaScript

```javascript
function findMaxAdjacentDifference(arr) {
    let maxDiff = 0;

    for (let i = 1; i < arr.length; i++) {
        let diff = Math.abs(arr[i] - arr[i - 1]);

        if (diff > maxDiff) {
            maxDiff = diff;
        }
    }

    return maxDiff;
}

console.log(findMaxAdjacentDifference([10, 15, 7, 20, 12]));
```

## Java

```java
public static int findMaxAdjacentDifference(int[] arr) {
    int maxDiff = 0;

    for (int i = 1; i < arr.length; i++) {
        int diff = Math.abs(arr[i] - arr[i - 1]);

        if (diff > maxDiff) {
            maxDiff = diff;
        }
    }

    return maxDiff;
}
```

## Complexity
- Time: O(n)
- Space: O(1)

## Pattern
**Neighbor comparison + best-so-far**

---

# 15. Find Smallest Positive Number

## Problem
Find the smallest positive number. If there is no positive number, return `-1`.

### Example
```text
Input:  [-5, 10, -2, 7, 3, -8, 4]
Output: 3
```

## JavaScript

```javascript
function findSmallestPositive(arr) {
    let min = Infinity;

    for (let i of arr) {
        if (i > 0 && i < min) {
            min = i;
        }
    }

    if (min === Infinity) {
        return -1;
    }

    return min;
}

console.log(findSmallestPositive([-5, 10, -2, 7, 3, -8, 4]));
```

## Java

```java
public static int findSmallestPositive(int[] arr) {
    int min = Integer.MAX_VALUE;

    for (int i : arr) {
        if (i > 0 && i < min) {
            min = i;
        }
    }

    if (min == Integer.MAX_VALUE) {
        return -1;
    }

    return min;
}
```

## Complexity
- Time: O(n)
- Space: O(1)

## Pattern
**Condition + best-so-far**

### Memory Hook
> Filter valid values → track the best valid value.

---

# 16. Find Largest Negative Number

## Problem
Find the largest negative number. If there is no negative number, return `-1`.

### Example
```text
Input:  [10, -5, -2, 7, -8, -3, 4]
Output: -2
```

## JavaScript

```javascript
function findLargestNegative(arr) {
    let max = -Infinity;

    for (let i of arr) {
        if (i < 0 && i > max) {
            max = i;
        }
    }

    if (max === -Infinity) {
        return -1;
    }

    return max;
}

console.log(findLargestNegative([10, -5, -2, 7, -8, -3, 4]));
```

## Java

```java
public static int findLargestNegative(int[] arr) {
    int max = Integer.MIN_VALUE;

    for (int i : arr) {
        if (i < 0 && i > max) {
            max = i;
        }
    }

    if (max == Integer.MIN_VALUE) {
        return -1;
    }

    return max;
}
```

## Complexity
- Time: O(n)
- Space: O(1)

## Pattern
**Condition + maximum-so-far**

---

# 17. Move All Zeros to the End

## Problem
Move all zeros to the end while maintaining the relative order of non-zero elements.

Do it in-place.

### Example
```text
Input:
[0, 1, 0, 3, 12]

Output:
[1, 3, 12, 0, 0]
```

## JavaScript

```javascript
function moveZerosToEnd(arr) {
    let position = 0;

    // Move non-zero elements forward
    for (let i = 0; i < arr.length; i++) {
        if (arr[i] !== 0) {
            arr[position] = arr[i];
            position++;
        }
    }

    // Fill remaining positions with zeros
    while (position < arr.length) {
        arr[position] = 0;
        position++;
    }

    return arr;
}

console.log(moveZerosToEnd([0, 1, 0, 3, 12]));
```

## Java

```java
import java.util.Arrays;

public static int[] moveZerosToEnd(int[] arr) {
    int position = 0;

    // Move non-zero elements forward
    for (int i = 0; i < arr.length; i++) {
        if (arr[i] != 0) {
            arr[position] = arr[i];
            position++;
        }
    }

    // Fill remaining positions with zeros
    while (position < arr.length) {
        arr[position] = 0;
        position++;
    }

    return arr;
}
```

Example Java usage:

```java
int[] arr = {0, 1, 0, 3, 12};

int[] result = moveZerosToEnd(arr);

System.out.println(Arrays.toString(result));
```

Output:

```text
[1, 3, 12, 0, 0]
```

## Complexity
- Time: O(n)
- Space: O(1)

## Pattern
**Two pointers — scanner + placement pointer**

### Memory Hook

```text
i        → scans the array
position → tells where the next non-zero goes
```

---

# Important Patterns Learned

## 1. Accumulator

Used for:
- Sum
- Count

```javascript
let result = 0;
```

Traverse and update.

---

## 2. Best-So-Far

Used for:
- Maximum
- Minimum
- Second largest
- Largest negative
- Smallest positive
- Maximum adjacent difference

Typical structure:

```javascript
let best = initialValue;

for (let i of arr) {
    if (condition) {
        best = i;
    }
}
```

---

## 3. Early Return

Used when one result is enough.

Example:

```javascript
for (let i of arr) {
    if (i <= 0) {
        return false;
    }
}
return true;
```

Memory hook:

> Find failure → return immediately.

---

## 4. First vs Last Occurrence

### First

```javascript
if (arr[i] === target) {
    return i;
}
```

### Last

```javascript
let last = -1;

for (...) {
    if (arr[i] === target) {
        last = i;
    }
}

return last;
```

Memory hook:

> First → stop early  
> Last → keep searching

---

## 5. Neighbor Comparison

Used for:
- Checking sorted array
- Adjacent differences

```javascript
arr[i]
arr[i - 1]
```

Usually start from:

```javascript
i = 1
```

because index `0` has no previous element.

---

## 6. Two-Pointer Technique

Reverse array:

```javascript
let left = 0;
let right = arr.length - 1;
```

Move zeros:

```javascript
let i = 0;
let position = 0;
```

Two-pointer does not necessarily mean pointers at opposite ends. It means using two variables to track positions for a purpose.

---

# Variable Placement Rule

One of the important things you learned:

> **If a variable needs to remember something across iterations → create it outside the loop.**

> **If a variable is only needed for the current iteration → create it inside the loop.**

Example:

```javascript
let max = -Infinity; // remembers previous best

for (let i of arr) {
    let diff = Math.abs(i); // current calculation only

    if (diff > max) {
        max = diff;
    }
}
```

### Common examples

| Variable | Usually | Reason |
|---|---|---|
| `count` | Outside | Remembers count |
| `sum` | Outside | Accumulates result |
| `max` | Outside | Remembers best |
| `min` | Outside | Remembers best |
| `position` | Outside | Remembers placement |
| `diff` | Inside | Current calculation |
| `current` | Inside | Current element/calculation |
| `temp` | Inside | Temporary value |

### Memory Hook

> **Outside = memory across iterations**  
> **Inside = temporary/current work**

---

# Edge Cases You Practiced

For array problems, remember to test:

1. Empty array — only if constraints allow it
2. One element
3. Two elements
4. All elements equal
5. Positive numbers
6. Negative numbers
7. Zero
8. Duplicates
9. Target not found
10. Target appears multiple times
11. Target at first position
12. Target at last position
13. Already sorted array
14. Reverse sorted array
15. All zeros
16. No zeros

---

# Problem-Solving Checklist

Before coding, ask:

```text
1. What exactly is the problem asking?
2. What is the input?
3. What is the output?
4. What are the constraints?
5. What are the edge cases?
6. Can I solve it with one loop?
7. What pattern does this problem use?
8. Which variables need to remember information?
9. Can I return early?
10. What is the time complexity?
11. What is the space complexity?
```

---

# Complexity Quick Reference

| Complexity | Common Example |
|---|---|
| O(1) | Direct array access |
| O(n) | One loop through array |
| O(n²) | Nested loops |
| O(log n) | Binary search |
| O(n log n) | Efficient sorting |

### Most of your current problems

Almost all were:

```text
Time:  O(n)
Space: O(1)
```

because you generally scan the array once and use only a few variables.

---

# Java vs JavaScript Quick Reference

## Array declaration

### JavaScript

```javascript
let arr = [10, 20, 30];
```

### Java

```java
int[] arr = {10, 20, 30};
```

## Array length

### JavaScript

```javascript
arr.length
```

### Java

```java
arr.length
```

## Equality

### JavaScript

```javascript
arr[i] === target
```

### Java

```java
arr[i] == target
```

## Loop

### JavaScript

```javascript
for (let i of arr) {
    // code
}
```

### Java

```java
for (int i : arr) {
    // code
}
```

## Print array

### JavaScript

```javascript
console.log(arr);
```

### Java

```java
System.out.println(Arrays.toString(arr));
```

Remember to import:

```java
import java.util.Arrays;
```

---

# Final Revision Challenge

Try solving these again **without looking at the answers**:

1. Sum of array
2. Maximum element
3. Count positive/negative/zero
4. Second largest
5. Reverse array
6. Count even numbers
7. Target exists
8. Find target index
9. First occurrence
10. Last occurrence
11. Count target occurrences
12. All elements positive
13. Array sorted
14. Maximum adjacent difference
15. Smallest positive
16. Largest negative
17. Move zeros to end

The goal is not to memorize the code.

The goal is to recognize the pattern:

```text
Problem
   ↓
Understand
   ↓
Identify pattern
   ↓
Choose variables
   ↓
Code
   ↓
Test edge cases
   ↓
Analyze complexity
```
