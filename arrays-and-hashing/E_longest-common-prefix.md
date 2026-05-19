**Link:** https://leetcode.com/problems/longest-common-prefix/description/

---

## Problem Translation

Given an array of strings, find the longest common prefix of these strings (the longest contiguous substring starting from the beginning to an index i that exactly matches the contiguous substrings for all other strings starting from their respective beginnings up to index i).

---

## Brute Force Solution

N/A

---

## Optimal Solution

1. We take note of the first string and we have a `validIndex` variable that takes note of the end index of our longest common prefix. It is first set to 0 (first character of our first string).
2. We then have a double for loop.
   - Outer loop loops through the length of our first string
   - Inner loop loops through every string in the `strs` array.
3. In our inner loop, we check every single string's character at `validIndex`. Is it the same with the character at `validIndex` of our first string? If all pass, we increment the `validIndex` by 1. If any check fails, we instantly return the substring of the first string from index 0 up to `validIndex`.

We also ensure we add a check in our inner loop to ensure our `validIndex` is not greater than the length of the string that we are currently iterating at. This prevents any array out of bound errors.

---

## Code for Optimal Solution

```python
class Solution:
    def longestCommonPrefix(self, strs: List[str]) -> str:
        validIndex = 0
        firstStr = strs[0]

        for i in range(len(firstStr)):
            baselineChar = firstStr[validIndex]
            for s in strs:
                if validIndex >= len(s) or s[validIndex] != baselineChar:
                    return firstStr[0:validIndex]
            validIndex += 1

        return firstStr[0:validIndex]

```

---

## Complexity Analysis

- **Time Complexity:** $O(n * m)$ — A double for loop is used, We loop through n (length of first string) and we do m work each iteration (loop through array of strings).
- **Space Complexity:** $O(1)$ — Only variables are used.

---

## Post-Mortem

- This problem was initially challenging but what helped made it alot clearer was really taking the time to step through the iterations one by one.
