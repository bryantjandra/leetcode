**Link:** https://leetcode.com/problems/concatenation-of-array/

---

## Problem Translation

Given an array of length n called nums, we want to have a new array of size 2n where nums is duplicated and appended to the end of itself.

---

## Brute Force Solution

1. We can instantiate a new array of size 2n (our result array).
2. Loop using index i from 0 to 2n, where our `result[i]` is assigned the value of `nums[i % len(nums)]` in order to cleanly loop through the original array twice.
3. Return our result array.

- **Time Complexity:** $O(n)$
- **Space Complexity:** $O(n)$

---

## Optimal Solution

We can utilize Python's built-in list concatenation operator (+) to create a completely new list of nums concatenated with itself. The standard implementation of Python (CPython) executes this operator using highly optimized C code.

In general, utilizing Python's standard library tools and built-in operators is significantly faster than executing a manual `for` loop because it leverages these low-level optimizations. Instead of evaluating and processing elements one by one, the C implementation calculates the total required memory once, allocates it, and performs a direct block-copy of the data.

Both brute force and optimal solutions are still $O(n)$. However, using the `+` operator is still faster in absolute time and much cleaner to write.

---

## Code for Optimal Solution

```python
class Solution:
    def getConcatenation(self, nums: List[int]) -> List[int]:
        return nums + nums
```

---

## Complexity Analysis

- **Time Complexity:** $O(n)$ — To concatenate the list, the interpreter must read and copy all N elements from the original array into a memory location.
- **Space Complexity:** $O(n)$ — Our result array of size 2N must be allocated into memory. Since we drop constants in asymptotic analysis, this simplifies to O(n).

---

## Post-Mortem

- Python's built-in list operations (e.g. `+` and `extend()`) are highly optimized. Whenever a problem requires direct copying or appending, we should prioritize using these standard library tools over writing custom loops.
