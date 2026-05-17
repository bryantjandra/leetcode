**Link: https://leetcode.com/problems/valid-anagram/description/**

---

## Problem Translation

Given two strings, return true if they have the exact same number of character counts and false otherwise.

---

## Brute Force Solution

Sorting both strings. If both strings are anagrams for each other, sorting them should yield the exact same string.

This however takes $O(n log n)$.

---

## Optimal Solution

We can utilize the ASCII mapping of characters to integers to use a standard list as a **frequency array**. The indices of the array serves as the ASCII values of the characters, and the values stored at those indices represent the count of that character.

1. Initialize a list of size 256 where every value is set to 0.
2. For every character in string s, translate it to its ASCII value. Use that ASCII value as the index for our frequency array and increment whatever the value is by 1.
3. For every character in string t, translate it to its ASCII value. Use that ASCII value as the index for our frequency array and decrement whatever the value is by 1.

If these two strings are truly anagrams, each increment of a characters count will be offset by a decrement. The frequency array should then have all its values set to 0. If any of its values are not 0, return False. Otherwise, return True.

---

## Code for Optimal Solution

```python
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        if len(s) != len(t):
            return False
        characterCount = [0] * 256
        for c in s:
            characterCount[ord(c)] += 1

        for c in t:
            characterCount[ord(c)] -= 1

        for c in characterCount:
            if c != 0:
                return False
        return True
```

---

## Complexity Analysis

- **Time Complexity:** $O(n+m)$ — n is length of string s, m is length of string t. We need to loop through both strings regardless. However the check at the top (checking if both strings are of equal length) would yield $O(n)$ as both strings would be of same length.

- **Space Complexity:** $O(1)$ — Constant as our frequency array is of fixed size (256). It does not scale relative to the size of the inputs.

---

## Post-Mortem

- When dealing with character frequencies where the character set is fixed and small (26 lowercase English characters or 256 ASCII characters), a fixed size array is faster and more memory-efficient than a HashMap. Arrays avoid the overhead of computing hash functions and resolving collisions.
