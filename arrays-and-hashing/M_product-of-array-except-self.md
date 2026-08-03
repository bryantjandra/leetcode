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

## Follow-Up Question on LC

- How to optimize to $O(1)$ space complexity? --> The output array does not count as extra space for space complexity analysis.

```python
class Solution:
    def productExceptSelf(self, nums: List[int]) -> List[int]:
        result = [1] * len(nums)
        for i in range(1, len(nums)):
            result[i] = nums[i-1] * result[i-1]

        suffix = 1
        for i in range(len(nums) - 1, -1, -1):
            result[i] = result[i] * suffix
            suffix = suffix * nums[i]

        return result
```

- In order to optimize to $O(1)$ space complexity, we remove the use of the two arrays (prefix and suffix). We instead utilize the actual output array as a substitute. 

- We first calculate the prefix products like how we would normally do, but then we just store them directly in our output array. We then loop backwards like how we would calculate our suffix product array, but we also keep track of a running suffix variable. 

- This running suffix variable keeps track of the product of all the elements to the right so far, as we are iterating backwards through the `nums` array.

- We then ensure we update this running suffix variable as we loop backwards, and we also ensure we update the output array (multiply the prefix product with the suffix variable in order to get the product of all elements except for this specific element). 

## Revisited 

Count: 1