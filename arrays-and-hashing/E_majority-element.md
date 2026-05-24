**Link:** https://leetcode.com/problems/majority-element/

---

## Problem Translation

Given an array `nums`, return the most frequent element that appears in `nums`. It is essentialy the element that appears more than `n/2` times where `n` is the length of `nums`.

---

## Brute Force Solution

Utilize a hashmap to count the frequencies of each element and keep track of the current maximum whilst looping over the `nums` array.

Time Complexity would be $O(n)$, but Space Complexity would be $O(n)$ as well.

---

## Optimal Solution

Utilize the Boyer-Moore Voting algorithm. Because the problem guarantees a majority element exists, it mathematically guarantees that the majority element wil survive any 1-to-1 cancellation with all other elements combined.

1. We keep track of the current candidate by using a count variable associated to it.
2. As we loop through the `nums` array, if we encounter an element that is not equal to our current candidate, we decrement the count. If it is the same, we increment our count.
3. If the count reaches 0, we swap the current candidate with the current element that we are iterating over.

When we finish iterating over the `nums` array, the resulting candidate will thus be the majority element.

---

## Code for Optimal Solution

```python
class Solution:
    def majorityElement(self, nums: List[int]) -> int:
        candidate = 0
        count = 0
        for num in nums:
            if count == 0:
                candidate = num
            if num == candidate:
                count += 1
            else:
                count -= 1


        return candidate


```

---

## Complexity Analysis

- **Time Complexity:** $O(n)$ — Looping through the entire `nums` array once.
- **Space Complexity:** $O(1)$ — No auxiliary data structures were used. Only variables.

---

## Post-Mortem

N/A.
