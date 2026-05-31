**Link:** https://leetcode.com/problems/sort-colors/

---

## Problem Translation

Essentially sort it such that all 0's are the beginning, all 1's are in the middle, and al 2's are at the end of the array.

---

## Brute Force Solution

Sort using library sorting function, or use Counting Sort (two passes however instead of just one pass).

---

## Optimal Solution

We can utilize a two-pointer strategy where the invariant is that all the integers to and including the left pointer will all be 0's and all the integers to and after the right pointer will all be 2's.

The 1's will then elegantly fall into place into the middle of the array.

We can achieve this by just iterating through the array:

1. Whenever we spot a `0`, we swap with whatever the integer is at the left pointer. Then increment the left pointer and our iterator.
2. Whenever we spot a `2`, we swap with whatever the integer is at the right pointer. Then decrement the right pointer.
   - It is important here that we actually do not increment our iterator just yet. This is because at any point in time, whenever we are swapping with the element at the right pointer, that element can either be a `0`, `1`, or `2`. If its a `1`, Thus, we have to rerun both the checks above in order to ensure all our elements are in the correct location. We can do this by simply not incrementing our iterator just yet.
   - The reason why it is safe to increment our iterator when Case (1) happens is because: The element that is swapped into i is guaranteed to be 1 if l < i (because all 2s got sent right of r and all 0s got sent left of l) and it is guaranteed to be 0 if l=i because that would mean nums[l] and nums[i] are literally the same slot.
3. Whenever it's neither `0` or `2` (meaning its a `1`), just let it be and increment our iterator.

---

## Code for Optimal Solution

```python
class Solution:
    def sortColors(self, nums: List[int]) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        l, r = 0, len(nums) - 1
        i = 0
        while i <= r:
            if nums[i] == 0:
                temp = nums[i]
                nums[i] = nums[l]
                nums[l] = temp
                l += 1
                i += 1
            elif nums[i] == 2:
                temp = nums[i]
                nums[i] = nums[r]
                nums[r] = temp
                r -= 1
            else:
                i += 1
```

---

## Complexity Analysis

- **Time Complexity:** $O(n)$ — One pass through the `nums` array.
- **Space Complexity:** $O(1)$ — No auxiliary space was used.

---

## Post-Mortem

N/A.
