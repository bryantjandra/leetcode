**Link:** https://leetcode.com/problems/product-of-array-except-self/description/

---

## Problem Translation

For every element in `nums` array, we want the product of all the other elements excluding the current element. We also cannot use the division operation.

---

## Brute Force Solution

N/A.

## Optimal Solution

We can have two arrays: a prefix array and a suffix array. 

Prefix Array: Contains the product of all the elements to the left of this particular element in `nums` array. 
Suffix Array: Contains the product of all the elements to the right of this particular element in `nums` array. 

It's important to note that the first element has nothing to its left, hence by default it's prefix value is set to 1. Same goes with the last element's suffix value.

In order to get the product of all elements except for a particular element in the `nums` array, all we have to do is multiply the product of all elements to the left **with** the product of all elements to the right. 

---

## Code for Optimal Solution

```python
class Solution:
    def productExceptSelf(self, nums: List[int]) -> List[int]:
        prefix = [1] * len(nums)
        suffix = [1] * len(nums)
        for i in range(1, len(nums)):
            prefix[i] = prefix[i-1] * nums[i-1]
        
        for i in range(len(nums) - 2, -1, -1):
            suffix[i] = suffix[i+1] * nums[i+1]
        
        res = [0] * len(nums)
        for i in range(len(nums)):
            res[i] = prefix[i] * suffix[i]
        
        return res



# for nums = [1,2,3,4]
# prefix should be: [1, 1, 2, 6]
# suffix should be: [24, 12, 4, 1]

```

---

## Complexity Analysis

- **Time Complexity:** $O(n)$ — We loop though the `nums` array of length n 3 times, and since this is a constant amount, the time complexity is $O(n)$ overall. 
- **Space Complexity:** $O(n)$ — We are using an array of the length n to store the result. 

---

## Post-Mortem

N/A.

