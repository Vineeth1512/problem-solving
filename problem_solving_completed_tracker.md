# Problem-Solving Completed Tracker

**Status:** This tracker summarizes the problems practiced before the
current lesson.\
**Languages:** JavaScript and Java.\
**Next problem:** Remove duplicates from a sorted array in place --- not
completed yet.

## Checklist

### Level 1 --- Array basics

-   [x] Sum array elements
-   [x] Find maximum
-   [x] Count positive, negative, and zero values
-   [x] Find second-largest distinct value
-   [x] Reverse array in place
-   [x] Count even numbers
-   [x] Check if target exists
-   [x] Find target index
-   [x] First occurrence
-   [x] Last occurrence
-   [x] Count occurrences
-   [x] Check whether all elements are positive
-   [x] Check ascending sorted order
-   [x] Maximum absolute difference between adjacent values
-   [x] Smallest positive value
-   [x] Largest negative value
-   [x] Move zeros to end, preserving nonzero order

### Level 2 --- Number problems

-   [x] Palindrome number
-   [x] Armstrong number
-   [x] Prime number
-   [x] Perfect number
-   [x] Count factors
-   [x] GCD using Euclidean algorithm
-   [x] LCM
-   [x] GCD of an array
-   [x] LCM of an array
-   [x] Fibonacci series
-   [x] Fibonacci number at index `n`
-   [x] Factorial
-   [x] Strong number
-   [x] Automorphic number

### Level 3 --- Array patterns / two pointers

-   [x] Reverse array with two pointers
-   [x] Two Sum in a sorted array
-   [x] Palindrome array
-   [x] Move zeros with scanner/placement pointers

------------------------------------------------------------------------

# 1. Array basics --- approaches

  -----------------------------------------------------------------------
  Problem                             Approach
  ----------------------------------- -----------------------------------
  Sum                                 Add each element to a running
                                      total.

  Maximum                             Track the largest value seen so
                                      far.

  Count signs                         Use separate counters for positive,
                                      negative, and zero values.

  Second largest                      Track the largest and
                                      second-largest distinct values.

  Reverse                             Swap opposite ends, then move both
                                      pointers inward.

  Count evens                         Count values where
                                      `value % 2 === 0`.

  Target exists                       Linear search; return `true`
                                      immediately when found.

  Target index                        Return matching index, or `-1`.

  First occurrence                    Return the first matching index
                                      immediately.

  Last occurrence                     Keep updating the answer for every
                                      match.

  Count occurrences                   Increase a counter for every match.

  All positive                        Return `false` if any value is
                                      `<= 0`.

  Sorted ascending                    Compare each value with the
                                      previous value.

  Maximum adjacent difference         Compare neighbors and track the
                                      maximum absolute difference.

  Smallest positive                   Track the smallest value greater
                                      than zero.

  Largest negative                    Track the negative value closest to
                                      zero.

  Move zeros                          Scan with `right`; `left` marks
                                      where the next nonzero goes.
  -----------------------------------------------------------------------

## JavaScript solutions

``` javascript
function sumArray(a) {
  let sum = 0;
  for (const x of a) sum += x;
  return sum;
}

function maxArray(a) {
  if (a.length === 0) return null;
  let max = a[0];
  for (let i = 1; i < a.length; i++) {
    if (a[i] > max) max = a[i];
  }
  return max;
}

function countSigns(a) {
  let positive = 0, negative = 0, zero = 0;
  for (const x of a) {
    if (x > 0) positive++;
    else if (x < 0) negative++;
    else zero++;
  }
  return { positive, negative, zero };
}

function secondLargest(a) {
  let largest = -Infinity, second = -Infinity;
  for (const x of a) {
    if (x > largest) {
      second = largest;
      largest = x;
    } else if (x < largest && x > second) {
      second = x;
    }
  }
  return second === -Infinity ? null : second;
}

function reverseArray(a) {
  let left = 0, right = a.length - 1;
  while (left < right) {
    [a[left], a[right]] = [a[right], a[left]];
    left++;
    right--;
  }
  return a;
}

function countEvens(a) {
  let count = 0;
  for (const x of a) if (x % 2 === 0) count++;
  return count;
}

function contains(a, target) {
  for (const x of a) if (x === target) return true;
  return false;
}

function findIndex(a, target) {
  for (let i = 0; i < a.length; i++) {
    if (a[i] === target) return i;
  }
  return -1;
}

function firstOccurrence(a, target) {
  for (let i = 0; i < a.length; i++) {
    if (a[i] === target) return i;
  }
  return -1;
}

function lastOccurrence(a, target) {
  let answer = -1;
  for (let i = 0; i < a.length; i++) {
    if (a[i] === target) answer = i;
  }
  return answer;
}

function countOccurrences(a, target) {
  let count = 0;
  for (const x of a) if (x === target) count++;
  return count;
}

function allPositive(a) {
  for (const x of a) if (x <= 0) return false;
  return true;
}

function isSortedAscending(a) {
  for (let i = 1; i < a.length; i++) {
    if (a[i] < a[i - 1]) return false;
  }
  return true;
}

function maxAdjacentDifference(a) {
  if (a.length < 2) return null;
  let maxDiff = 0;
  for (let i = 1; i < a.length; i++) {
    maxDiff = Math.max(maxDiff, Math.abs(a[i] - a[i - 1]));
  }
  return maxDiff;
}

function smallestPositive(a) {
  let answer = Infinity;
  for (const x of a) if (x > 0 && x < answer) answer = x;
  return answer === Infinity ? null : answer;
}

function largestNegative(a) {
  let answer = -Infinity;
  for (const x of a) if (x < 0 && x > answer) answer = x;
  return answer === -Infinity ? null : answer;
}

function moveZeros(a) {
  let left = 0;
  for (let right = 0; right < a.length; right++) {
    if (a[right] !== 0) {
      [a[left], a[right]] = [a[right], a[left]];
      left++;
    }
  }
  return a;
}
```

## Java solutions

``` java
import java.util.Arrays;

public class ArrayPractice {
    static int sumArray(int[] a) {
        int sum = 0;
        for (int x : a) sum += x;
        return sum;
    }

    static Integer maxArray(int[] a) {
        if (a.length == 0) return null;
        int max = a[0];
        for (int i = 1; i < a.length; i++) {
            if (a[i] > max) max = a[i];
        }
        return max;
    }

    // Result positions: [positive count, negative count, zero count]
    static int[] countSigns(int[] a) {
        int positive = 0, negative = 0, zero = 0;
        for (int x : a) {
            if (x > 0) positive++;
            else if (x < 0) negative++;
            else zero++;
        }
        return new int[]{positive, negative, zero};
    }

    static Integer secondLargest(int[] a) {
        long largest = Long.MIN_VALUE, second = Long.MIN_VALUE;
        for (int x : a) {
            if (x > largest) {
                second = largest;
                largest = x;
            } else if (x < largest && x > second) {
                second = x;
            }
        }
        return second == Long.MIN_VALUE ? null : (int) second;
    }

    static int[] reverseArray(int[] a) {
        int left = 0, right = a.length - 1;
        while (left < right) {
            int temp = a[left];
            a[left] = a[right];
            a[right] = temp;
            left++;
            right--;
        }
        return a;
    }

    static int countEvens(int[] a) {
        int count = 0;
        for (int x : a) if (x % 2 == 0) count++;
        return count;
    }

    static boolean contains(int[] a, int target) {
        for (int x : a) if (x == target) return true;
        return false;
    }

    static int findIndex(int[] a, int target) {
        for (int i = 0; i < a.length; i++) {
            if (a[i] == target) return i;
        }
        return -1;
    }

    static int firstOccurrence(int[] a, int target) {
        for (int i = 0; i < a.length; i++) {
            if (a[i] == target) return i;
        }
        return -1;
    }

    static int lastOccurrence(int[] a, int target) {
        int answer = -1;
        for (int i = 0; i < a.length; i++) {
            if (a[i] == target) answer = i;
        }
        return answer;
    }

    static int countOccurrences(int[] a, int target) {
        int count = 0;
        for (int x : a) if (x == target) count++;
        return count;
    }

    static boolean allPositive(int[] a) {
        for (int x : a) if (x <= 0) return false;
        return true;
    }

    static boolean isSortedAscending(int[] a) {
        for (int i = 1; i < a.length; i++) {
            if (a[i] < a[i - 1]) return false;
        }
        return true;
    }

    static Integer maxAdjacentDifference(int[] a) {
        if (a.length < 2) return null;
        int maxDiff = 0;
        for (int i = 1; i < a.length; i++) {
            maxDiff = Math.max(maxDiff, Math.abs(a[i] - a[i - 1]));
        }
        return maxDiff;
    }

    static Integer smallestPositive(int[] a) {
        Integer answer = null;
        for (int x : a) {
            if (x > 0 && (answer == null || x < answer)) answer = x;
        }
        return answer;
    }

    static Integer largestNegative(int[] a) {
        Integer answer = null;
        for (int x : a) {
            if (x < 0 && (answer == null || x > answer)) answer = x;
        }
        return answer;
    }

    static int[] moveZeros(int[] a) {
        int left = 0;
        for (int right = 0; right < a.length; right++) {
            if (a[right] != 0) {
                int temp = a[left];
                a[left] = a[right];
                a[right] = temp;
                left++;
            }
        }
        return a;
    }

    public static void main(String[] args) {
        int[] a = {0, 1, 0, 3, 12};
        System.out.println(Arrays.toString(moveZeros(a))); // [1, 3, 12, 0, 0]
    }
}
```

------------------------------------------------------------------------

# 2. Number problems --- approaches

  -----------------------------------------------------------------------
  Problem                             Approach
  ----------------------------------- -----------------------------------
  Palindrome                          Reverse the digits and compare with
                                      the original.

  Armstrong                           Sum each digit raised to the number
                                      of digits.

  Prime                               Test divisors while `i * i <= n`.

  Perfect                             Sum proper divisors, excluding the
                                      number itself.

  Count factors                       Count values from 1 to `n` that
                                      divide `n`.

  GCD                                 Repeatedly replace `(a, b)` with
                                      `(b, a % b)`.

  LCM                                 `abs((a / gcd(a,b)) * b)`.

  Array GCD/LCM                       Start with first element; combine
                                      it with each next element.

  Fibonacci series                    Keep two previous values and update
                                      them each turn.

  Fibonacci at index                  Iterate from `F(0)=0`, `F(1)=1`.

  Factorial                           Multiply integers from 2 to `n`.

  Strong number                       Sum factorials of the digits and
                                      compare to original.

  Automorphic                         Square the number and check whether
                                      the square ends with the original
                                      number.
  -----------------------------------------------------------------------

## JavaScript solutions

``` javascript
function reverseNumber(n) {
  let x = Math.abs(n), reversed = 0;
  while (x > 0) {
    reversed = reversed * 10 + (x % 10);
    x = Math.floor(x / 10);
  }
  return n < 0 ? -reversed : reversed;
}

function isPalindromeNumber(n) {
  return n >= 0 && n === reverseNumber(n);
}

function isArmstrong(n) {
  if (n < 0) return false;
  const digits = String(n).split("").map(Number);
  let sum = 0;
  for (const digit of digits) sum += digit ** digits.length;
  return sum === n;
}

function isPrime(n) {
  if (n < 2) return false;
  for (let i = 2; i * i <= n; i++) {
    if (n % i === 0) return false;
  }
  return true;
}

function isPerfect(n) {
  if (n <= 1) return false;
  let sum = 1;
  for (let i = 2; i * i <= n; i++) {
    if (n % i === 0) {
      sum += i;
      if (i !== n / i) sum += n / i;
    }
  }
  return sum === n;
}

function countFactors(n) {
  if (n <= 0) return 0;
  let count = 0;
  for (let i = 1; i <= n; i++) if (n % i === 0) count++;
  return count;
}

function gcd(a, b) {
  a = Math.abs(a);
  b = Math.abs(b);
  while (b !== 0) {
    const remainder = a % b;
    a = b;
    b = remainder;
  }
  return a;
}

function lcm(a, b) {
  if (a === 0 || b === 0) return 0;
  return Math.abs((a / gcd(a, b)) * b);
}

function gcdArray(a) {
  if (a.length === 0) return null;
  let result = Math.abs(a[0]);
  for (let i = 1; i < a.length; i++) result = gcd(result, a[i]);
  return result;
}

function lcmArray(a) {
  if (a.length === 0) return null;
  let result = Math.abs(a[0]);
  for (let i = 1; i < a.length; i++) result = lcm(result, a[i]);
  return result;
}

function fibonacciSeries(count) {
  const result = [];
  let a = 0, b = 1;
  for (let i = 0; i < count; i++) {
    result.push(a);
    [a, b] = [b, a + b];
  }
  return result;
}

// Zero-based: fibonacciAt(0) = 0, fibonacciAt(1) = 1
function fibonacciAt(n) {
  if (n < 0 || !Number.isInteger(n)) return null;
  let a = 0, b = 1;
  for (let i = 0; i < n; i++) [a, b] = [b, a + b];
  return a;
}

function factorial(n) {
  if (n < 0 || !Number.isInteger(n)) return null;
  let result = 1;
  for (let i = 2; i <= n; i++) result *= i;
  return result;
}

function digitFactorial(d) {
  let result = 1;
  for (let i = 2; i <= d; i++) result *= i;
  return result;
}

function isStrong(n) {
  if (n < 0) return false;
  let x = n, sum = 0;
  do {
    sum += digitFactorial(x % 10);
    x = Math.floor(x / 10);
  } while (x > 0);
  return sum === n;
}

function isAutomorphic(n) {
  if (n < 0) return false;
  const digits = String(n).length;
  return (n * n) % (10 ** digits) === n;
}
```

## Java solutions

``` java
public class NumberPractice {
    static long reverseNumber(long n) {
        long x = Math.abs(n), reversed = 0;
        while (x > 0) {
            reversed = reversed * 10 + x % 10;
            x /= 10;
        }
        return n < 0 ? -reversed : reversed;
    }

    static boolean isPalindromeNumber(long n) {
        return n >= 0 && n == reverseNumber(n);
    }

    static boolean isArmstrong(int n) {
        if (n < 0) return false;
        String s = String.valueOf(n);
        int power = s.length();
        long sum = 0;
        for (int i = 0; i < s.length(); i++) {
            int digit = s.charAt(i) - '0';
            sum += (long) Math.pow(digit, power);
        }
        return sum == n;
    }

    static boolean isPrime(int n) {
        if (n < 2) return false;
        for (int i = 2; i * i <= n; i++) {
            if (n % i == 0) return false;
        }
        return true;
    }

    static boolean isPerfect(int n) {
        if (n <= 1) return false;
        int sum = 1;
        for (int i = 2; i * i <= n; i++) {
            if (n % i == 0) {
                sum += i;
                if (i != n / i) sum += n / i;
            }
        }
        return sum == n;
    }

    static int countFactors(int n) {
        if (n <= 0) return 0;
        int count = 0;
        for (int i = 1; i <= n; i++) if (n % i == 0) count++;
        return count;
    }

    static long gcd(long a, long b) {
        a = Math.abs(a);
        b = Math.abs(b);
        while (b != 0) {
            long remainder = a % b;
            a = b;
            b = remainder;
        }
        return a;
    }

    static long lcm(long a, long b) {
        if (a == 0 || b == 0) return 0;
        return Math.abs((a / gcd(a, b)) * b);
    }

    static Long gcdArray(int[] a) {
        if (a.length == 0) return null;
        long result = Math.abs((long) a[0]);
        for (int i = 1; i < a.length; i++) result = gcd(result, a[i]);
        return result;
    }

    static Long lcmArray(int[] a) {
        if (a.length == 0) return null;
        long result = Math.abs((long) a[0]);
        for (int i = 1; i < a.length; i++) result = lcm(result, a[i]);
        return result;
    }

    static long[] fibonacciSeries(int count) {
        if (count < 0) throw new IllegalArgumentException("count must be >= 0");
        long[] result = new long[count];
        long a = 0, b = 1;
        for (int i = 0; i < count; i++) {
            result[i] = a;
            long next = a + b;
            a = b;
            b = next;
        }
        return result;
    }

    static Long fibonacciAt(int n) {
        if (n < 0) return null;
        long a = 0, b = 1;
        for (int i = 0; i < n; i++) {
            long next = a + b;
            a = b;
            b = next;
        }
        return a;
    }

    static Long factorial(int n) {
        if (n < 0) return null;
        long result = 1;
        for (int i = 2; i <= n; i++) result *= i;
        return result;
    }

    static int digitFactorial(int digit) {
        int result = 1;
        for (int i = 2; i <= digit; i++) result *= i;
        return result;
    }

    static boolean isStrong(int n) {
        if (n < 0) return false;
        int x = n, sum = 0;
        do {
            sum += digitFactorial(x % 10);
            x /= 10;
        } while (x > 0);
        return sum == n;
    }

    static boolean isAutomorphic(long n) {
        if (n < 0) return false;
        long square = n * n;
        long divisor = 10, x = n;
        while (x >= 10) {
            divisor *= 10;
            x /= 10;
        }
        return square % divisor == n;
    }

    public static void main(String[] args) {
        System.out.println(isPalindromeNumber(121)); // true
        System.out.println(isArmstrong(153));         // true
        System.out.println(isPrime(17));              // true
        System.out.println(isPerfect(28));            // true
        System.out.println(gcd(48, 18));              // 6
        System.out.println(lcm(4, 6));                // 12
        System.out.println(isStrong(145));             // true
        System.out.println(isAutomorphic(25));         // true
    }
}
```

------------------------------------------------------------------------

# 3. Two-pointer problems --- approach and solutions

## Reverse array

Use `left = 0`, `right = length - 1`; swap and move both inward.

## Two Sum in a sorted array

Start at both ends. If the sum is too small, increment `left`; if too
large, decrement `right`. This solution returns indices.

## Palindrome array

Compare both ends. Return `false` on the first mismatch; otherwise move
inward and return `true`.

## Move zeros

`right` scans the array; `left` marks the next place for a nonzero. Swap
and advance `left` whenever `right` finds a nonzero.

### JavaScript

``` javascript
function twoSumSorted(a, target) {
  let left = 0, right = a.length - 1;
  while (left < right) {
    const sum = a[left] + a[right];
    if (sum === target) return [left, right]; // indices
    if (sum < target) left++;
    else right--;
  }
  return [];
}

function isPalindromeArray(a) {
  let left = 0, right = a.length - 1;
  while (left < right) {
    if (a[left] !== a[right]) return false;
    left++;
    right--;
  }
  return true;
}
```

### Java

``` java
import java.util.Arrays;

public class TwoPointersPractice {
    // Returns indices, not values.
    static int[] twoSumSorted(int[] a, int target) {
        int left = 0, right = a.length - 1;
        while (left < right) {
            int sum = a[left] + a[right];
            if (sum == target) return new int[]{left, right};
            if (sum < target) left++;
            else right--;
        }
        return new int[0];
    }

    static boolean isPalindromeArray(int[] a) {
        int left = 0, right = a.length - 1;
        while (left < right) {
            if (a[left] != a[right]) return false;
            left++;
            right--;
        }
        return true;
    }

    public static void main(String[] args) {
        int[] a = {1, 2, 4, 6, 8, 9};
        System.out.println(Arrays.toString(twoSumSorted(a, 10))); // [0, 5]
        System.out.println(isPalindromeArray(new int[]{1, 2, 3, 2, 1})); // true
    }
}
```

------------------------------------------------------------------------

# 4. Complexity and reminders

  Problem/pattern                                     Time   Extra space
  ------------------------------------- ------------------ -------------
  Single array scan                                   O(n)          O(1)
  Reverse with two pointers                           O(n)          O(1)
  Move zeros in place                                 O(n)          O(1)
  Prime check with `i * i <= n`                      O(√n)          O(1)
  Iterative Euclidean GCD                 O(log(min(a,b)))          O(1)
  Fibonacci series stored in an array                 O(n)          O(n)
  Fibonacci at index, iterative                       O(n)          O(1)

-   **First occurrence:** return immediately when found.
-   **Last occurrence:** keep updating the answer and return after the
    loop.
-   `return` exits the entire function, not just the loop.
-   Confirm whether a pair problem asks for **values** or **indices**.
-   In-place means modifying the original array.
-   Moving zeros must preserve the order of nonzero values.
-   `fibonacciSeries(7)` means seven terms; `fibonacciAt(7)` means the
    value at zero-based index 7.
-   Automorphic examples: `5`, `6`, and `25`; `36` is not automorphic
    because `36² = 1296` does not end in `36`.

## Next problem --- not done yet

**Remove duplicates from a sorted array in place.**

``` javascript
let arr = [1, 1, 2, 2, 3, 4, 4];

function removeDuplicates(arr) {
  // Modify arr in place.
  // Return k, the count of unique values.
}

let k = removeDuplicates(arr);
console.log(k);           // Expected: 4
console.log(arr.slice(0, k)); // Expected: [1, 2, 3, 4]
```

Pattern: **slow/fast pointers**. Try writing the logic yourself before
checking a solution.
