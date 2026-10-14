# Java & JavaScript Problem-Solving Practice Notes

**Current focus:** Problem solving, strings, loops, frequency counting,
and time/space complexity.

## 1. Foundations

-   Variables, data types, conditions, loops, functions/methods, arrays,
    strings, return values.
-   Dry-running code and translating logic between JavaScript and Java.
-   Time complexity: `O(1)`, `O(n)`, `O(n²)`, `O(log n)`.
-   Space complexity: additional memory used by an algorithm.
-   Two separate linear loops are generally `O(n)` overall; nested loops
    are often `O(n²)`.

## 2. Array Problems Practiced

-   Sum of an array
-   Find maximum and second-largest elements
-   Count positive numbers, negative numbers, and zeros
-   Count even numbers
-   Reverse an array using two pointers
-   Search for an element
-   First and last occurrence/index
-   Count occurrences
-   Check whether all elements are positive
-   Check whether an array is sorted
-   Adjacent differences
-   Smallest positive and largest negative values
-   Move zeros to the end
-   Palindrome array
-   Two Sum on a sorted array using two pointers
-   Binary search
-   Prefix sums and range-sum queries
-   Fixed-size sliding window and introduction to variable-size sliding
    window
-   Maximum stock profit
-   Kadane's algorithm / maximum subarray sum
-   Maximum product subarray

### Patterns

-   **Traversal:** visit each element.
-   **Two pointers:** move two indices according to a condition.
-   **Frequency counting:** store how often values appear.
-   **Prefix sum:** reuse accumulated sums for range queries.
-   **Sliding window:** update a moving range without recalculating
    everything.
-   **Binary search:** repeatedly halve a sorted search range.

## 3. Number Problems Practiced

-   Palindrome number
-   Armstrong number
-   Prime number check
-   Perfect number
-   GCD using the Euclidean algorithm
-   GCD of an array
-   LCM of an array
-   Fibonacci sequence and Fibonacci at position `n`
-   Strong number
-   Automorphic number

### Number reminders

-   Preserve the original number if you need it later.
-   `number % 10` gets the last digit; integer division by `10` removes
    it.
-   For prime checking, testing divisors while `i * i <= n` is
    sufficient.
-   Dry-run with a small example.

## 4. String Problems Practiced

### Count characters

Traverse the string and count each character position.

### Reverse a string

-   Traverse from the last index to the first and append characters.
-   Or traverse forward and prepend characters.
-   JavaScript strings are immutable, so two-pointer swapping needs a
    mutable character array.

### Palindrome string

-   Compare characters from both ends with two pointers.
-   Advanced version ignores case, spaces, punctuation, and symbols;
    only English letters and digits are compared.
-   `continue` skips the rest of the current iteration; move the
    relevant pointer before continuing.

### Count vowels and consonants

Count `a`, `e`, `i`, `o`, and `u` as vowels. Check that a character is a
letter before counting it as a consonant; do not count spaces, digits,
or punctuation.

### Count occurrences

Count how many times a target character appears. Example: `"Banana"`
with target `"A"` (case-insensitive) gives `3`.

### First non-repeating character

1.  Count every character's frequency using a JavaScript object or Java
    `HashMap`.
2.  Traverse the string again.
3.  Return the first character with frequency `1`.
4.  Return `null` if none exists. Examples: `"aabbcde"` → `c`; `"swiss"`
    → `w`; `"aabb"` → `null`.

### First repeating character

Traverse left to right and track characters already seen. Return the
first character encountered for a second time. Examples: `"abca"` → `a`;
`"hello"` → `l`; `"abcd"` → `null`.

### Anagrams

Check whether two strings have the same characters with the same
frequencies, regardless of order. The practiced version ignores case and
spaces. 1. Normalize both strings. 2. If lengths differ, return `false`.
3. Count characters in the first string. 4. Decrease counts while
reading the second string. 5. Return `false` if a character is missing
or has no count left; otherwise return `true`. Examples: `"aab"` vs
`"abb"` → `false`; `"Dormitory"` vs `"Dirty room"` → `true` when
ignoring case and spaces.

### Most frequent character

1.  Normalize case and remove spaces if required.
2.  Count frequencies.
3.  Initialize `maxFreq` and `result`.
4.  Update both when a character's frequency is strictly greater than
    `maxFreq`.
5.  Return the result after the loop. Tie rule practiced: use `>` rather
    than `>=` to keep the first character that reaches the maximum.
    Examples: `"programming"` → `r`; `"success"` → `s`; `"abcd"` → `a`.

### Remove duplicate characters

Keep only each character's first occurrence while preserving order.
Examples: `"programming"` → `"progamin"`; `"hello"` → `"helo"`;
`"aabbcc"` → `"abc"`; `"abcd"` → `"abcd"`.

Approaches discussed: 1. JavaScript object to track seen characters. 2.
Java `Set<Character>` / `HashSet`. 3. Java `boolean[]` indexed by
character value. 4. Java `indexOf()`. 5. Nested loops that compare each
input character against characters already in the result.

Basic nested-loop approach: - Read one character from the input. -
Compare it with each character already in the result. - If found, skip
it; otherwise append it. - Nested-loop duplicate checking is typically
`O(n²)`. Repeated Java string concatenation may add copying overhead;
`StringBuilder` is usually more efficient.

## 5. JavaScript Concepts Used

-   String indexing (`str[i]`) and `str.length`
-   Functions and `return`
-   Objects as key-value stores
-   Dynamic object keys: `freq[ch]`
-   Frequency counting with objects
-   `toLowerCase()` and `replace()` for normalization when allowed
-   `undefined` checks for missing object properties
-   `continue` and `break`
-   Strict equality (`===`)
-   Truthy/falsy values, type conversion, and coercion
-   Arrays and two-pointer patterns

**Object reminder:** If `ch` contains `"a"`, `obj[ch]` accesses key
`"a"`, while `obj.ch` accesses the literal key `"ch"`.

## 6. Java Concepts Used

-   Methods, return types, `String`, `char`, `charAt(i)`, and `length()`
-   `HashMap<Character, Integer>` for frequency counting
-   `Map.containsKey()`, `Map.get()`, and `Map.put()`
-   `HashSet` / `Set` for unique-character tracking
-   `boolean[]` for character tracking
-   `StringBuilder` and `append()`
-   Primitive `char` versus wrapper `Character`
-   Returning `null` from a method returning `Character` or `String`
-   `break`, `continue`, and nested loops
-   Generics such as `Set<Character>` and `Map<Character, Integer>`

Prefer generic types: - `Set<Character> seen = new HashSet<>();` -
`Map<Character, Integer> freq = new HashMap<>();`

## 7. Important Lessons

-   One loop can count frequencies; another can use those frequencies to
    find an answer.
-   `maxFreq` stores the highest frequency found so far; `result` stores
    the corresponding character.
-   Update a candidate inside the loop, but return after the loop when
    all candidates must be checked.
-   `>` preserves the first character to reach the maximum; `>=` can
    change tie behavior.
-   `HashMap` / JavaScript objects are useful for frequency counting.
-   `Set` tracks whether a value has appeared.
-   A boolean flag such as `duplicate` can record whether a match was
    found.
-   `break` exits a loop early.
-   Clarify "no built-in methods": Java's `length()` and `charAt()` are
    basic access methods commonly still needed to traverse a string.

## 8. Practice Checklist

### Arrays

-   [ ] Sum, maximum, and second largest
-   [ ] Count positive, negative, and zero values
-   [ ] Reverse using two pointers
-   [ ] First/last occurrence and frequency
-   [ ] Move zeros to the end
-   [ ] Palindrome array
-   [ ] Two Sum
-   [ ] Binary search
-   [ ] Prefix sums
-   [ ] Sliding window
-   [ ] Kadane's algorithm

### Numbers

-   [ ] Palindrome number
-   [ ] Armstrong number
-   [ ] Prime number
-   [ ] Perfect number
-   [ ] GCD and LCM
-   [ ] Fibonacci
-   [ ] Strong number
-   [ ] Automorphic number

### Strings

-   [x] Count characters
-   [x] Reverse a string
-   [x] Palindrome with ignored punctuation and case
-   [x] Count vowels and consonants
-   [x] Count occurrences
-   [x] First non-repeating character
-   [x] First repeating character
-   [x] Anagram check
-   [x] Most frequent character
-   [x] Remove duplicate characters
-   [ ] Reverse words in a sentence
-   [ ] Check string rotation
-   [ ] Longest substring without repeating characters
-   [ ] Group anagrams
-   [ ] Longest palindromic substring

## 9. Workflow for Every Problem

1.  Understand the problem and examples.
2.  Write expected input and output.
3.  Solve one small example manually.
4.  Choose a simple approach.
5.  Write the JavaScript solution.
6.  Translate the logic into Java.
7.  Dry-run using a table of variable values.
8.  Test normal, empty, and edge-case inputs.
9.  Analyze time and space complexity.
10. Optimize only after understanding the basic solution.

**Current milestone:** String traversal, frequency counting, duplicate
detection, and translating logic between JavaScript and Java.
