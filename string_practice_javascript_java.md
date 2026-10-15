# Yesterday's String Problem-Solving Practice
## JavaScript and Java Solutions

This file contains only the string problems practiced yesterday. Each problem has a JavaScript solution and a Java solution.

---

## 1. Count Characters

**Example:** `"hello"` → `5`

### JavaScript
```javascript
function countCharacters(str) {
    let count = 0;
    for (let i = 0; i < str.length; i++) count++;
    return count;
}
console.log(countCharacters("hello")); // 5
```

### Java
```java
class Main {
    static int countCharacters(String str) {
        int count = 0;
        for (int i = 0; i < str.length(); i++) count++;
        return count;
    }
    public static void main(String[] args) {
        System.out.println(countCharacters("hello")); // 5
    }
}
```

---

## 2. Reverse a String

**Example:** `"hello"` → `"olleh"`

### JavaScript
```javascript
function reverseString(str) {
    let result = "";
    for (let i = str.length - 1; i >= 0; i--) result += str[i];
    return result;
}
console.log(reverseString("hello")); // "olleh"
```

### Java
```java
class Main {
    static String reverseString(String str) {
        String result = "";
        for (int i = str.length() - 1; i >= 0; i--) {
            result += str.charAt(i);
        }
        return result;
    }
    public static void main(String[] args) {
        System.out.println(reverseString("hello")); // olleh
    }
}
```

---

## 3. Palindrome String (ignore case, spaces, and punctuation)

**Example:** `"A man, a plan, a canal: Panama!"` → `true`

### JavaScript
```javascript
function isAlphaNumeric(ch) {
    return (ch >= "a" && ch <= "z") || (ch >= "0" && ch <= "9");
}

function isPalindrome(str) {
    str = str.toLowerCase();
    let left = 0;
    let right = str.length - 1;

    while (left < right) {
        if (!isAlphaNumeric(str[left])) {
            left++;
            continue;
        }
        if (!isAlphaNumeric(str[right])) {
            right--;
            continue;
        }
        if (str[left] !== str[right]) return false;
        left++;
        right--;
    }
    return true;
}
console.log(isPalindrome("A man, a plan, a canal: Panama!")); // true
```

### Java
```java
class Main {
    static boolean isAlphaNumeric(char ch) {
        return (ch >= 'a' && ch <= 'z') || (ch >= '0' && ch <= '9');
    }

    static boolean isPalindrome(String str) {
        str = str.toLowerCase();
        int left = 0, right = str.length() - 1;

        while (left < right) {
            if (!isAlphaNumeric(str.charAt(left))) {
                left++;
                continue;
            }
            if (!isAlphaNumeric(str.charAt(right))) {
                right--;
                continue;
            }
            if (str.charAt(left) != str.charAt(right)) return false;
            left++;
            right--;
        }
        return true;
    }

    public static void main(String[] args) {
        System.out.println(isPalindrome("A man, a plan, a canal: Panama!")); // true
    }
}
```

---

## 4. Count Vowels and Consonants

**Example:** `"hello"` → Vowels: `2`, Consonants: `3`. Non-English-letter characters are ignored.

### JavaScript
```javascript
function countVowelsConsonants(str) {
    str = str.toLowerCase();
    let vowels = 0, consonants = 0;

    for (let i = 0; i < str.length; i++) {
        let ch = str[i];
        if (ch >= "a" && ch <= "z") {
            if ("aeiou".includes(ch)) vowels++;
            else consonants++;
        }
    }
    return { vowels, consonants };
}
console.log(countVowelsConsonants("hello")); // { vowels: 2, consonants: 3 }
```

### Java
```java
class Main {
    static void countVowelsConsonants(String str) {
        str = str.toLowerCase();
        int vowels = 0, consonants = 0;

        for (int i = 0; i < str.length(); i++) {
            char ch = str.charAt(i);
            if (ch >= 'a' && ch <= 'z') {
                if (ch == 'a' || ch == 'e' || ch == 'i' || ch == 'o' || ch == 'u') {
                    vowels++;
                } else {
                    consonants++;
                }
            }
        }
        System.out.println("Vowels: " + vowels);
        System.out.println("Consonants: " + consonants);
    }
    public static void main(String[] args) {
        countVowelsConsonants("hello");
    }
}
```

---

## 5. Count Occurrences of a Character

**Example:** `"javascript"`, target `'a'` → `2`

### JavaScript
```javascript
function countOccurrences(str, target) {
    let count = 0;
    for (let i = 0; i < str.length; i++) {
        if (str[i] === target) count++;
    }
    return count;
}
console.log(countOccurrences("javascript", "a")); // 2
```

### Java
```java
class Main {
    static int countOccurrences(String str, char target) {
        int count = 0;
        for (int i = 0; i < str.length(); i++) {
            if (str.charAt(i) == target) count++;
        }
        return count;
    }
    public static void main(String[] args) {
        System.out.println(countOccurrences("javascript", 'a')); // 2
    }
}
```

---

## 6. First Non-Repeating Character

**Example:** `"aabbcddee"` → `'c'`

### JavaScript
```javascript
function firstNonRepeatingChar(str) {
    const freq = {};
    for (let i = 0; i < str.length; i++) {
        let ch = str[i];
        if (freq[ch] === undefined) freq[ch] = 1;
        else freq[ch]++;
    }
    for (let i = 0; i < str.length; i++) {
        if (freq[str[i]] === 1) return str[i];
    }
    return null;
}
console.log(firstNonRepeatingChar("aabbcddee")); // "c"
```

### Java
```java
import java.util.HashMap;
import java.util.Map;

class Main {
    static Character firstNonRepeatingChar(String str) {
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
    public static void main(String[] args) {
        System.out.println(firstNonRepeatingChar("aabbcddee")); // c
    }
}
```

---

## 7. First Repeating Character

Returns the first character encountered whose earlier occurrence has already been seen.

**Example:** `"abca"` → `'a'`

### JavaScript
```javascript
function firstRepeatingChar(str) {
    const seen = {};
    for (let i = 0; i < str.length; i++) {
        let ch = str[i];
        if (seen[ch] === true) return ch;
        seen[ch] = true;
    }
    return null;
}
console.log(firstRepeatingChar("abca")); // "a"
```

### Java
```java
import java.util.HashSet;
import java.util.Set;

class Main {
    static Character firstRepeatingChar(String str) {
        Set<Character> seen = new HashSet<>();
        for (int i = 0; i < str.length(); i++) {
            char ch = str.charAt(i);
            if (seen.contains(ch)) return ch;
            seen.add(ch);
        }
        return null;
    }
    public static void main(String[] args) {
        System.out.println(firstRepeatingChar("abca")); // a
    }
}
```

---

## 8. Check Whether Two Strings Are Anagrams

Ignores case and ordinary spaces.

**Example:** `"Dormitory"` and `"Dirty room"` → `true`

### JavaScript
```javascript
function areAnagrams(str1, str2) {
    str1 = str1.toLowerCase().replace(/ /g, "");
    str2 = str2.toLowerCase().replace(/ /g, "");
    if (str1.length !== str2.length) return false;

    const freq = {};
    for (let i = 0; i < str1.length; i++) {
        let ch = str1[i];
        freq[ch] = (freq[ch] || 0) + 1;
    }
    for (let i = 0; i < str2.length; i++) {
        let ch = str2[i];
        if (freq[ch] === undefined || freq[ch] === 0) return false;
        freq[ch]--;
    }
    return true;
}
console.log(areAnagrams("Dormitory", "Dirty room")); // true
```

### Java
```java
import java.util.HashMap;
import java.util.Map;

class Main {
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
    public static void main(String[] args) {
        System.out.println(areAnagrams("Dormitory", "Dirty room")); // true
    }
}
```

---

## 9. Most Frequent Character

If characters tie for the highest frequency, returns the one whose first occurrence is earliest in the string.

**Example:** `"success"` → `'s'`

### JavaScript
```javascript
function mostFrequentChar(str) {
    if (str.length === 0) return null;
    const freq = {};

    for (let i = 0; i < str.length; i++) {
        let ch = str[i];
        freq[ch] = (freq[ch] || 0) + 1;
    }

    let maxFreq = 0;
    let result = str[0];
    for (let i = 0; i < str.length; i++) {
        let ch = str[i];
        if (freq[ch] > maxFreq) {
            maxFreq = freq[ch];
            result = ch;
        }
    }
    return result;
}
console.log(mostFrequentChar("success")); // "s"
```

### Java
```java
import java.util.HashMap;
import java.util.Map;

class Main {
    static Character mostFrequentChar(String str) {
        if (str.length() == 0) return null;
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
    public static void main(String[] args) {
        System.out.println(mostFrequentChar("success")); // s
    }
}
```

---

## 10. Remove Duplicate Characters

Preserves the order of first appearances.

**Example:** `"programming"` → `"progamin"`

### JavaScript
```javascript
function removeDuplicates(str) {
    let result = "";
    const seen = {};
    for (let i = 0; i < str.length; i++) {
        let ch = str[i];
        if (seen[ch] === undefined) {
            result += ch;
            seen[ch] = true;
        }
    }
    return result;
}
console.log(removeDuplicates("programming")); // "progamin"
```

### Java
```java
import java.util.HashSet;
import java.util.Set;

class Main {
    static String removeDuplicates(String str) {
        StringBuilder result = new StringBuilder();
        Set<Character> seen = new HashSet<>();

        for (int i = 0; i < str.length(); i++) {
            char ch = str.charAt(i);
            if (!seen.contains(ch)) {
                result.append(ch);
                seen.add(ch);
            }
        }
        return result.toString();
    }
    public static void main(String[] args) {
        System.out.println(removeDuplicates("programming")); // progamin
    }
}
```

---

## 11. Reverse Words in a Sentence

Reverses word order, not letters inside each word. Assumes single spaces between words.

**Example:** `"I love Java"` → `"Java love I"`

### JavaScript
```javascript
function reverseWords(str) {
    let result = "";
    let word = "";
    for (let i = str.length - 1; i >= 0; i--) {
        if (str[i] !== " ") {
            word = str[i] + word;
        } else {
            result += word + " ";
            word = "";
        }
    }
    result += word;
    return result;
}
console.log(reverseWords("I love Java")); // "Java love I"
```

### Java
```java
class Main {
    static String reverseWords(String str) {
        String result = "";
        String word = "";
        for (int i = str.length() - 1; i >= 0; i--) {
            if (str.charAt(i) != ' ') {
                word = str.charAt(i) + word;
            } else {
                result += word + " ";
                word = "";
            }
        }
        result += word;
        return result;
    }
    public static void main(String[] args) {
        System.out.println(reverseWords("I love Java")); // Java love I
    }
}
```

---

## 12. Count Words in a String

Counts the beginning of each word, so multiple spaces do not add extra words.

**Example:** `"  I   love   Java  "` → `3`

### JavaScript
```javascript
function countWords(str) {
    let count = 0;
    for (let i = 0; i < str.length; i++) {
        if (str[i] !== " " && (i === 0 || str[i - 1] === " ")) {
            count++;
        }
    }
    return count;
}
console.log(countWords("I love JavaScript")); // 3
console.log(countWords("  I   love   Java  ")); // 3
console.log(countWords("")); // 0
```

### Java
```java
class Main {
    static int countWords(String str) {
        int count = 0;
        for (int i = 0; i < str.length(); i++) {
            if (str.charAt(i) != ' ' &&
                (i == 0 || str.charAt(i - 1) == ' ')) {
                count++;
            }
        }
        return count;
    }
    public static void main(String[] args) {
        System.out.println(countWords("I love JavaScript")); // 3
        System.out.println(countWords("  I   love   Java  ")); // 3
        System.out.println(countWords("")); // 0
    }
}
```

---

## Revision Checklist

- [ ] Count characters
- [ ] Reverse a string
- [ ] Check a palindrome
- [ ] Count vowels and consonants
- [ ] Count character occurrences
- [ ] First non-repeating character
- [ ] First repeating character
- [ ] Check anagrams
- [ ] Most frequent character
- [ ] Remove duplicate characters
- [ ] Reverse words in a sentence
- [ ] Count words in a string
