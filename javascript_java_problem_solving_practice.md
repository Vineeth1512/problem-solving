# JavaScript and Java Problem-Solving Practice Notes

These notes collect the array, number, and string problems practiced so
far. Practice each problem in JavaScript first, then write the Java
version without looking.

## Practice method

1.  Understand the input and expected output.
2.  Explain the approach in your own words.
3.  Dry-run with a small example.
4.  Write the code independently.
5.  State time and space complexity.
6.  Test edge cases: empty input, one element, duplicates, and negative
    values where relevant.

------------------------------------------------------------------------

# 1. Arrays

## 1.1 Sum of an array

**JavaScript**

``` javascript
function sumArray(arr) {
    let sum = 0;
    for (let i = 0; i < arr.length; i++) sum += arr[i];
    return sum;
}
console.log(sumArray([1, 2, 3, 4])); // 10
```

**Java**

``` java
static int sumArray(int[] arr) {
    int sum = 0;
    for (int i = 0; i < arr.length; i++) sum += arr[i];
    return sum;
}
// sumArray(new int[]{1, 2, 3, 4}) -> 10
```

Time O(n), extra space O(1).

## 1.2 Find the maximum

**JavaScript**

``` javascript
function findMax(arr) {
    if (arr.length === 0) return null;
    let max = arr[0];
    for (let i = 1; i < arr.length; i++) {
        if (arr[i] > max) max = arr[i];
    }
    return max;
}
```

**Java**

``` java
static Integer findMax(int[] arr) {
    if (arr.length == 0) return null;
    int max = arr[0];
    for (int i = 1; i < arr.length; i++) {
        if (arr[i] > max) max = arr[i];
    }
    return max;
}
```

Time O(n), extra space O(1).

## 1.3 Second-largest distinct element

**JavaScript**

``` javascript
function secondLargest(arr) {
    let largest = -Infinity;
    let second = -Infinity;

    for (let value of arr) {
        if (value > largest) {
            second = largest;
            largest = value;
        } else if (value < largest && value > second) {
            second = value;
        }
    }
    return second === -Infinity ? null : second;
}
console.log(secondLargest([10, 5, 8, 10])); // 8
```

**Java**

``` java
static Integer secondLargest(int[] arr) {
    Integer largest = null, second = null;

    for (int value : arr) {
        if (largest == null || value > largest) {
            if (largest != null) second = largest;
            largest = value;
        } else if (value < largest && (second == null || value > second)) {
            second = value;
        }
    }
    return second;
}
```

Time O(n), extra space O(1).

## 1.4 Count positive, negative, and zero values

**JavaScript**

``` javascript
function countSigns(arr) {
    let positive = 0, negative = 0, zeros = 0;
    for (let value of arr) {
        if (value > 0) positive++;
        else if (value < 0) negative++;
        else zeros++;
    }
    return { positive, negative, zeros };
}
```

**Java**

``` java
static void countSigns(int[] arr) {
    int positive = 0, negative = 0, zeros = 0;
    for (int value : arr) {
        if (value > 0) positive++;
        else if (value < 0) negative++;
        else zeros++;
    }
    System.out.println("Positive: " + positive);
    System.out.println("Negative: " + negative);
    System.out.println("Zeros: " + zeros);
}
```

Time O(n), extra space O(1).

## 1.5 Reverse an array in place (two pointers)

**JavaScript**

``` javascript
function reverseArray(arr) {
    let left = 0, right = arr.length - 1;
    while (left < right) {
        const temp = arr[left];
        arr[left] = arr[right];
        arr[right] = temp;
        left++;
        right--;
    }
    return arr;
}
```

**Java**

``` java
static int[] reverseArray(int[] arr) {
    int left = 0, right = arr.length - 1;
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

Time O(n), extra space O(1).

## 1.6 Move zeros to the end

**JavaScript**

``` javascript
function moveZeros(arr) {
    let position = 0;
    for (let i = 0; i < arr.length; i++) {
        if (arr[i] !== 0) {
            const temp = arr[position];
            arr[position] = arr[i];
            arr[i] = temp;
            position++;
        }
    }
    return arr;
}
console.log(moveZeros([0, 1, 0, 3, 12])); // [1, 3, 12, 0, 0]
```

**Java**

``` java
static int[] moveZeros(int[] arr) {
    int position = 0;
    for (int i = 0; i < arr.length; i++) {
        if (arr[i] != 0) {
            int temp = arr[position];
            arr[position] = arr[i];
            arr[i] = temp;
            position++;
        }
    }
    return arr;
}
```

Time O(n), extra space O(1).

## 1.7 Two Sum in a sorted array

**JavaScript**

``` javascript
function twoSumSorted(arr, target) {
    let left = 0, right = arr.length - 1;
    while (left < right) {
        const sum = arr[left] + arr[right];
        if (sum === target) return [left, right];
        if (sum < target) left++;
        else right--;
    }
    return null;
}
```

**Java**

``` java
static int[] twoSumSorted(int[] arr, int target) {
    int left = 0, right = arr.length - 1;
    while (left < right) {
        int sum = arr[left] + arr[right];
        if (sum == target) return new int[]{left, right};
        if (sum < target) left++;
        else right--;
    }
    return null;
}
```

The array must be sorted. Time O(n), extra space O(1), excluding the
returned pair.

## 1.8 Binary search

**JavaScript**

``` javascript
function binarySearch(arr, target) {
    let left = 0, right = arr.length - 1;
    while (left <= right) {
        const mid = Math.floor(left + (right - left) / 2);
        if (arr[mid] === target) return mid;
        if (arr[mid] < target) left = mid + 1;
        else right = mid - 1;
    }
    return -1;
}
```

**Java**

``` java
static int binarySearch(int[] arr, int target) {
    int left = 0, right = arr.length - 1;
    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (arr[mid] == target) return mid;
        if (arr[mid] < target) left = mid + 1;
        else right = mid - 1;
    }
    return -1;
}
```

Requires sorted input. Time O(log n), extra space O(1).

------------------------------------------------------------------------

# 2. Number problems

## 2.1 Palindrome number

**JavaScript**

``` javascript
function isPalindromeNumber(n) {
    if (n < 0) return false;
    const original = n;
    let reversed = 0;
    while (n > 0) {
        const digit = n % 10;
        reversed = reversed * 10 + digit;
        n = Math.floor(n / 10);
    }
    return original === reversed;
}
```

**Java**

``` java
static boolean isPalindromeNumber(int n) {
    if (n < 0) return false;
    int original = n, reversed = 0;
    while (n > 0) {
        int digit = n % 10;
        reversed = reversed * 10 + digit;
        n /= 10;
    }
    return original == reversed;
}
```

Time O(log n), extra space O(1).

## 2.2 Armstrong number

A number is an Armstrong number when the sum of each digit raised to the
number of digits equals the original number.

**JavaScript**

``` javascript
function isArmstrong(n) {
    if (n < 0) return false;
    const original = n;
    const digits = String(n).length;
    let sum = 0, temp = n;
    while (temp > 0) {
        const digit = temp % 10;
        sum += digit ** digits;
        temp = Math.floor(temp / 10);
    }
    return sum === original;
}
console.log(isArmstrong(153)); // true
```

**Java**

``` java
static boolean isArmstrong(int n) {
    if (n < 0) return false;
    int original = n;
    int digits = String.valueOf(n).length();
    int sum = 0, temp = n;
    while (temp > 0) {
        int digit = temp % 10;
        sum += (int) Math.pow(digit, digits);
        temp /= 10;
    }
    return sum == original;
}
```

Time O(d), where d is the number of digits. Extra space O(1), excluding
digit-count conversion.

## 2.3 Prime number

**JavaScript**

``` javascript
function isPrime(n) {
    if (n < 2) return false;
    for (let i = 2; i * i <= n; i++) {
        if (n % i === 0) return false;
    }
    return true;
}
```

**Java**

``` java
static boolean isPrime(int n) {
    if (n < 2) return false;
    for (int i = 2; i * i <= n; i++) {
        if (n % i == 0) return false;
    }
    return true;
}
```

Time O(√n), extra space O(1). We only check up to the square root
because factors come in pairs.

## 2.4 Perfect number

A perfect number equals the sum of its positive divisors, excluding
itself. Example: 28 = 1 + 2 + 4 + 7 + 14.

**JavaScript**

``` javascript
function isPerfectNumber(n) {
    if (n <= 1) return false;
    let sum = 1;
    for (let i = 2; i * i <= n; i++) {
        if (n % i === 0) {
            sum += i;
            const pair = n / i;
            if (pair !== i) sum += pair;
        }
    }
    return sum === n;
}
```

**Java**

``` java
static boolean isPerfectNumber(int n) {
    if (n <= 1) return false;
    int sum = 1;
    for (int i = 2; i * i <= n; i++) {
        if (n % i == 0) {
            sum += i;
            int pair = n / i;
            if (pair != i) sum += pair;
        }
    }
    return sum == n;
}
```

Time O(√n), extra space O(1).

## 2.5 GCD (Euclidean algorithm)

**JavaScript**

``` javascript
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
console.log(gcd(24, 18)); // 6
```

**Java**

``` java
static int gcd(int a, int b) {
    a = Math.abs(a);
    b = Math.abs(b);
    while (b != 0) {
        int remainder = a % b;
        a = b;
        b = remainder;
    }
    return a;
}
```

Time O(log(min(a, b))) for positive inputs; extra space O(1).

## 2.6 Fibonacci sequence

**JavaScript**

``` javascript
function fibonacci(n) {
    if (n <= 0) return [];
    const result = [];
    let a = 0, b = 1;
    for (let i = 0; i < n; i++) {
        result.push(a);
        const next = a + b;
        a = b;
        b = next;
    }
    return result;
}
console.log(fibonacci(7)); // [0, 1, 1, 2, 3, 5, 8]
```

**Java**

``` java
static int[] fibonacci(int n) {
    if (n <= 0) return new int[0];
    int[] result = new int[n];
    int a = 0, b = 1;
    for (int i = 0; i < n; i++) {
        result[i] = a;
        int next = a + b;
        a = b;
        b = next;
    }
    return result;
}
```

Time O(n), output space O(n).

------------------------------------------------------------------------

# 3. String problems

## 3.1 Count characters

**JavaScript**

``` javascript
function countCharacters(str) {
    let count = 0;
    for (let i = 0; i < str.length; i++) count++;
    return count;
}
```

**Java**

``` java
static int countCharacters(String str) {
    int count = 0;
    for (int i = 0; i < str.length(); i++) count++;
    return count;
}
```

Time O(n), extra space O(1). For normal use, JavaScript `str.length` and
Java `str.length()` already give the length.

## 3.2 Reverse a string

**JavaScript**

``` javascript
function reverseString(str) {
    let result = "";
    for (let i = str.length - 1; i >= 0; i--) {
        result += str[i];
    }
    return result;
}
```

**Java**

``` java
static String reverseString(String str) {
    String result = "";
    for (int i = str.length() - 1; i >= 0; i--) {
        result += str.charAt(i);
    }
    return result;
}
```

Repeated Java string concatenation can make this O(n²); `StringBuilder`
improves Java performance to O(n). Output space O(n).

## 3.3 Palindrome string, ignoring case and punctuation

This example handles ASCII English letters and digits.

**JavaScript**

``` javascript
function isAlphaNumeric(ch) {
    return (ch >= "a" && ch <= "z") ||
           (ch >= "0" && ch <= "9");
}

function isPalindrome(str) {
    str = str.toLowerCase();
    let left = 0, right = str.length - 1;

    while (left < right) {
        const a = str[left], b = str[right];

        if (!isAlphaNumeric(a)) {
            left++;
            continue;
        }
        if (!isAlphaNumeric(b)) {
            right--;
            continue;
        }
        if (a !== b) return false;
        left++;
        right--;
    }
    return true;
}
console.log(isPalindrome("A man, a plan, a canal: Panama")); // true
```

**Java**

``` java
static boolean isAlphaNumeric(char ch) {
    return (ch >= 'a' && ch <= 'z') || (ch >= '0' && ch <= '9');
}

static boolean isPalindrome(String str) {
    str = str.toLowerCase();
    int left = 0, right = str.length() - 1;

    while (left < right) {
        char a = str.charAt(left), b = str.charAt(right);

        if (!isAlphaNumeric(a)) {
            left++;
            continue;
        }
        if (!isAlphaNumeric(b)) {
            right--;
            continue;
        }
        if (a != b) return false;
        left++;
        right--;
    }
    return true;
}
```

Time O(n), auxiliary space O(1) apart from lowercase conversion.
`continue` skips to the next loop iteration, so move the relevant
pointer first.

## 3.4 Count vowels and consonants

Only English letters are counted; spaces, numbers, and punctuation are
ignored.

**JavaScript**

``` javascript
function countVowelsAndConsonants(str) {
    str = str.toLowerCase();
    let vowels = 0, consonants = 0;

    for (let i = 0; i < str.length; i++) {
        const ch = str[i];
        if (ch >= "a" && ch <= "z") {
            if (ch === "a" || ch === "e" || ch === "i" ||
                ch === "o" || ch === "u") vowels++;
            else consonants++;
        }
    }
    return { vowels, consonants };
}
```

**Java**

``` java
static void countVowelsAndConsonants(String str) {
    str = str.toLowerCase();
    int vowels = 0, consonants = 0;

    for (int i = 0; i < str.length(); i++) {
        char ch = str.charAt(i);
        if (ch >= 'a' && ch <= 'z') {
            if (ch == 'a' || ch == 'e' || ch == 'i' ||
                ch == 'o' || ch == 'u') vowels++;
            else consonants++;
        }
    }
    System.out.println("Vowels: " + vowels);
    System.out.println("Consonants: " + consonants);
}
```

Time O(n), extra space O(1) apart from lowercase conversion.

## 3.5 Count occurrences of a character

**JavaScript**

``` javascript
function countOccurrences(str, target) {
    str = str.toLowerCase();
    target = target.toLowerCase();
    let count = 0;
    for (let i = 0; i < str.length; i++) {
        if (str[i] === target) count++;
    }
    return count;
}
console.log(countOccurrences("Banana", "A")); // 3
```

**Java**

``` java
static int countOccurrences(String str, char target) {
    str = str.toLowerCase();
    target = Character.toLowerCase(target);
    int count = 0;
    for (int i = 0; i < str.length(); i++) {
        if (str.charAt(i) == target) count++;
    }
    return count;
}
```

Time O(n), extra space O(1) apart from lowercase conversion.

## 3.6 First non-repeating character

**JavaScript**

``` javascript
function firstNonRepeating(str) {
    str = str.toLowerCase();
    const freq = {};

    for (let i = 0; i < str.length; i++) {
        const ch = str[i];
        if (freq[ch] === undefined) freq[ch] = 1;
        else freq[ch]++;
    }

    for (let i = 0; i < str.length; i++) {
        if (freq[str[i]] === 1) return str[i];
    }
    return null;
}
```

**Java**

``` java
import java.util.HashMap;
import java.util.Map;

static Character firstNonRepeating(String str) {
    str = str.toLowerCase();
    Map<Character, Integer> freq = new HashMap<>();

    for (int i = 0; i < str.length(); i++) {
        char ch = str.charAt(i);
        freq.put(ch, freq.getOrDefault(ch, 0) + 1);
    }

    for (int i = 0; i < str.length(); i++) {
        char ch = str.charAt(i);
        if (freq.get(ch) == 1) return ch;
    }
    return null;
}
```

Time O(n) average, extra space O(k) for distinct characters.

## 3.7 First repeating character

**JavaScript**

``` javascript
function firstRepeating(str) {
    str = str.toLowerCase();
    const seen = {};

    for (let i = 0; i < str.length; i++) {
        const ch = str[i];
        if (seen[ch] !== undefined) return ch;
        seen[ch] = true;
    }
    return null;
}
```

**Java**

``` java
import java.util.HashSet;
import java.util.Set;

static Character firstRepeating(String str) {
    str = str.toLowerCase();
    Set<Character> seen = new HashSet<>();

    for (int i = 0; i < str.length(); i++) {
        char ch = str.charAt(i);
        if (seen.contains(ch)) return ch;
        seen.add(ch);
    }
    return null;
}
```

Time O(n) average, extra space O(k).

## 3.8 Anagrams, ignoring case and spaces

**JavaScript**

``` javascript
function areAnagrams(str1, str2) {
    str1 = str1.toLowerCase().replace(/\s/g, "");
    str2 = str2.toLowerCase().replace(/\s/g, "");
    if (str1.length !== str2.length) return false;

    const freq = {};
    for (let i = 0; i < str1.length; i++) {
        const ch = str1[i];
        if (freq[ch] === undefined) freq[ch] = 1;
        else freq[ch]++;
    }

    for (let i = 0; i < str2.length; i++) {
        const ch = str2[i];
        if (freq[ch] === undefined || freq[ch] === 0) return false;
        freq[ch]--;
    }
    return true;
}
console.log(areAnagrams("Dormitory", "Dirty room")); // true
console.log(areAnagrams("aab", "abb")); // false
```

**Java**

``` java
import java.util.HashMap;
import java.util.Map;

static boolean areAnagrams(String str1, String str2) {
    str1 = str1.toLowerCase().replace(" ", "");
    str2 = str2.toLowerCase().replace(" ", "");
    if (str1.length() != str2.length()) return false;

    Map<Character, Integer> freq = new HashMap<>();
    for (int i = 0; i < str1.length(); i++) {
        char ch = str1.charAt(i);
        freq.put(ch, freq.getOrDefault(ch, 0) + 1);
    }

    for (int i = 0; i < str2.length(); i++) {
        char ch = str2.charAt(i);
        if (!freq.containsKey(ch) || freq.get(ch) == 0) return false;
        freq.put(ch, freq.get(ch) - 1);
    }
    return true;
}
```

Time O(n) average, extra space O(k). A frequency of zero means there are
no remaining occurrences of that character to match.

## 3.9 Most frequent character

Tie rule: keep the first character that reaches the maximum frequency.
Spaces are ignored.

**JavaScript**

``` javascript
function mostFrequentChar(str) {
    str = str.toLowerCase().replace(/\s/g, "");
    if (str.length === 0) return null;

    const freq = {};
    for (let i = 0; i < str.length; i++) {
        const ch = str[i];
        if (freq[ch] === undefined) freq[ch] = 1;
        else freq[ch]++;
    }

    let maxFreq = 0;
    let result = str[0];

    for (let i = 0; i < str.length; i++) {
        const ch = str[i];
        if (freq[ch] > maxFreq) {
            maxFreq = freq[ch];
            result = ch;
        }
    }
    return result;
}
console.log(mostFrequentChar("programming")); // "r"
console.log(mostFrequentChar("success")); // "s"
console.log(mostFrequentChar("Hello World")); // "l"
console.log(mostFrequentChar("abcd")); // "a"
```

**Java**

``` java
import java.util.HashMap;
import java.util.Map;

static Character mostFrequentChar(String str) {
    str = str.toLowerCase().replace(" ", "");
    if (str.isEmpty()) return null;

    Map<Character, Integer> freq = new HashMap<>();
    for (int i = 0; i < str.length(); i++) {
        char ch = str.charAt(i);
        freq.put(ch, freq.getOrDefault(ch, 0) + 1);
    }

    int maxFreq = 0;
    char result = str.charAt(0);

    for (int i = 0; i < str.length(); i++) {
        char ch = str.charAt(i);
        if (freq.get(ch) > maxFreq) {
            maxFreq = freq.get(ch);
            result = ch;
        }
    }
    return result;
}
```

Time O(n) average, extra space O(k). Use `>` (not `>=`) to preserve the
first character in a tie.

## 3.10 Remove duplicate characters

Keep the first occurrence of each character and preserve order.

**JavaScript**

``` javascript
function removeDuplicates(str) {
    let result = "";
    const seen = {};

    for (let i = 0; i < str.length; i++) {
        const ch = str[i];
        if (seen[ch] === undefined) {
            result += ch;
            seen[ch] = true;
        }
    }
    return result;
}
console.log(removeDuplicates("programming")); // "progamin"
console.log(removeDuplicates("hello")); // "helo"
console.log(removeDuplicates("aabbcc")); // "abc"
```

**Java --- with a Set**

``` java
import java.util.HashSet;
import java.util.Set;

static String removeDuplicates(String str) {
    Set<Character> seen = new HashSet<>();
    StringBuilder result = new StringBuilder();

    for (int i = 0; i < str.length(); i++) {
        char ch = str.charAt(i);
        if (seen.add(ch)) result.append(ch);
    }
    return result.toString();
}
```

**Java --- without a Set or tracking array**

``` java
static String removeDuplicatesWithoutSet(String str) {
    String result = "";

    for (int i = 0; i < str.length(); i++) {
        char ch = str.charAt(i);
        boolean duplicate = false;

        for (int j = 0; j < result.length(); j++) {
            if (result.charAt(j) == ch) {
                duplicate = true;
                break;
            }
        }

        if (!duplicate) result = result + ch;
    }
    return result;
}
```

The nested-loop version uses no search method or collection; it manually
checks each character against the result. Time is O(n²) for the checks,
and repeated string concatenation may add copying cost. The Set +
StringBuilder version is O(n) average.

------------------------------------------------------------------------

# 4. Patterns to remember

## Frequency counting

Use an object in JavaScript or a `Map` in Java when counting characters
or comparing frequencies.

## Two pointers

Use `left` and `right` moving toward each other for reversing arrays,
checking palindromes, and Two Sum on sorted arrays.

## Nested loops

Useful for direct comparisons and learning duplicate detection. Usually
O(n²).

## `continue`

Skips the rest of the current loop iteration. Move the relevant pointer
before using `continue`.

## Complexity quick reference

  Complexity   Example
  ------------ -------------------------------------
  O(1)         Read one array element by index
  O(log n)     Binary search
  O(n)         One pass through an array or string
  O(n log n)   Efficient comparison sorting
  O(n²)        Nested loops over the input

## JavaScript and Java differences

-   JavaScript array/string length: `arr.length`, `str.length`
-   Java array length: `arr.length`
-   Java string length: `str.length()`
-   JavaScript character access: `str[i]`
-   Java character access: `str.charAt(i)`
-   JavaScript frequency object: `freq[ch]`
-   Java map frequency: `freq.get(ch)`
-   Java strings are immutable; use `StringBuilder` for repeated
    appends.
-   JavaScript strings are also immutable; repeated concatenation can
    allocate new strings.

------------------------------------------------------------------------

# 5. Practice checklist

-   [ ] Sum of array
-   [ ] Maximum element
-   [ ] Second-largest distinct element
-   [ ] Count positive, negative, and zero values
-   [ ] Reverse array with two pointers
-   [ ] Move zeros to the end
-   [ ] Two Sum in a sorted array
-   [ ] Binary search
-   [ ] Palindrome number
-   [ ] Armstrong number
-   [ ] Prime number
-   [ ] Perfect number
-   [ ] GCD with Euclidean algorithm
-   [ ] Fibonacci sequence
-   [ ] Count string characters
-   [ ] Reverse a string
-   [ ] Palindrome string with punctuation handling
-   [ ] Count vowels and consonants
-   [ ] Count occurrences
-   [ ] First non-repeating character
-   [ ] First repeating character
-   [ ] Check anagrams
-   [ ] Most frequent character
-   [ ] Remove duplicate characters

**Suggested routine:** Solve one problem in JavaScript, then solve it
again in Java. Dry-run both versions and explain the time and space
complexity aloud.
