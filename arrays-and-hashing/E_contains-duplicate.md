**Link: https://leetcode.com/problems/contains-duplicate/**

---

## Problem Translation

We are given an array nums, if there are any duplicate elements in the nums array, we return True. Otherwise, we return False.

---

## Brute Force Solution

The optimal solution is pretty trivial. However, a possible brute-force solution involves sorting the initial array first, and then looping throug the sorted array whilst checking whether any adjacent elements are identical to each other.

This is however $O(nlog n)$ time.

---

## Optimal Solution

We can have a hashset. Loop through each element in the nums array, and for each element, we check the hashset first whether it contains that element. If our hashset already contains that element, it means its a duplicate and we return true. Otherwise, we add the element into our hashset.

If we are able to loop through the entire nums array without encountering a duplicate element, return false.

---

## Code for Optimal Solution

```python
class Solution:
    def containsDuplicate(self, nums: List[int]) -> bool:
        visited = set()
        for num in nums:
            if num in visited:
                return True
            visited.add(num)
        return False
```

---

## Complexity Analysis

- **Time Complexity:** $O(n)$ — Looping through nums array is $O(n)$ and checking/adding items to a hashset is $O(1)$.
- **Space Complexity:** $O(n)$ — Our hashset can contain at most n elements.

---

## Post-Mortem

N/A
