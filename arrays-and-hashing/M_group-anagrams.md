**Link:** https://leetcode.com/problems/group-anagrams/

---

## Problem Translation

Given an array of strings `strs`, we want to group any anagrams with each other.

---

## Brute Force Solution

Sorting each string and using the sorted version of that string as the key.

Time complexity would be $O(n * klogk)$ however, as we are iterating through the array of strings once, and in each iteration we do `klogk` work as we are sorting each string.

---

## Optimal Solution

Using intuition from the **Valid Anagram** problem, when strings are anagrams of each other, their frequency of characters are the exact same. We can then use a frequency array for each string to calculate each string's exact frequency of characters.

We utilize a hashmap (`defaultdict`). Our hashmap's keys will be each unique anagram's frequency array. The values will be a list containing the original strings in our `strs` array that essentially have the same frequency array as the key (meaning each string in this list are anagrams of each other as they share the same frequency array).

NOTE: It is important to cast the frequency array as a tuple in order for us to use it as keys in our hashmap. This is as Python lists are mutable whilst tuples are immutable.

---

## Code for Optimal Solution

```python
from collections import defaultdict

class Solution:
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
        myDict = defaultdict(list)
        for s in strs:
            freqArray = [0] * 256
            for c in s:
                freqArray[ord(c)] += 1
            myDict[tuple(freqArray)].append(s)

        return list(myDict.values())
```

---

## Complexity Analysis

- **Time Complexity:** $O(n * k)$ — We are iterating through the array of strings once, and in each iteration we do `k` work as we are iterating through each string.
- **Space Complexity:** $O(n * k)$ — We are storing all n strings, with each string having max length of k in our values.

---

## Post-Mortem

- myDict.values() returns a view object and not a list, It must be explicitly casted into a list before returning using `list()`.
- To calculate total space complexity, we ensure we add up the total space required for all keys with the total space required for all values.
