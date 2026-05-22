**Link:** https://leetcode.com/problems/remove-element/description/

---

## Problem Translation

Modify the array in-place so that all elements not equal to `val` are shifted to the front. Return the count of these valid elements (k). The elements remaining beyond index k do not matter.

---

## Brute Force Solution

1. Sort. Then swap all occurences of `val` with the elements at the end of the array using a decrementing pointer.
   - However, this is $O(n log n)$ Time Complexity.

2. Create a completely new array. Iterate through the original `nums` array, and if an element does not equal `val`, append it to the new array. Finally, copy the elements from the new array back into the original `nums` array.
   - However, this is $O(n)$ Space Complexity.

---

## Optimal Solution

We can just use two pointers, a left pointer at index 0 and a right pointer at the last index.

Whenever `nums[left]` is equal to val, we always want to be able to swap it with `nums[right]`.

However if `nums[right]` is also equal to val, we can't simply swap them. We need to be patient and ensure that `nums[right]` is not equal to `val`, we do this by decrementing the right pointer until `nums[right]` is not equal to val.

Only if `nums[left]` is equal to val AND `nums[right]` is not equal to val, we swap them.

If `nums[left]` is **not** equal to `val`, it is already in a valid position. We simply increment the `left` pointer to keep it and move on. We do not decrement the right pointer as if we do, we are potentially skipping over valid elements that should have been shifted to the front!

---

## Code for Optimal Solution

```python
class Solution:
    def removeElement(self, nums: List[int], val: int) -> int:
        left, right = 0, len(nums) - 1
        while left <= right:
            if nums[left] == val and nums[right] != val:
                temp = nums[left]
                nums[left] = nums[right]
                nums[right] = temp
                left += 1
                right -= 1
            elif nums[left] == val and nums[right] == val:
                right -= 1
            else:
                left += 1
        return left
```

---

## Complexity Analysis

- **Time Complexity:** $O(n)$ — Iterating through nums array once.
- **Space Complexity:** $O(1)$ — The array is modified in-place and only index pointers are used.

---

## Post-Mortem

N/A.
