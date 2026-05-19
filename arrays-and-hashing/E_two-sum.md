**Link:** https://leetcode.com/problems/two-sum/description/

---

## Problem Translation

We have a target number and a nums array. Our task is to find two unique indices in the nums array where the value of those indices sum up to target.

---

## Brute Force Solution

Use a double for loop and check every single unique two element combination. Check if they sum up to target or not.

- **Time Complexity:** $O(n^2)$, as a double for loop is utilized.
- **Space Complexity:** $O(1)$

---

## Optimal Solution

We utilize a hashmap in order to store elements of the nums array that we have seen so far. The keys of our hashmap will be the actual elements of the nums array, whilst the values will be the indices of those elements.

1. Enumerate through the nums array, taking note of the current index and the actual element
2. Perform a check whether we've seen the **complement** before in our hashmap. The complement is is the (target - actual element). If the complement exists in our hashmap, this simply means two unique indices do exist, and they do sum up to our target (complement from our hashmap is a previously seen value in our nums array + our current element = target).
3. If complement doesn't exist, we add as an entry to our hashmap: the current actual element as the key, the current index as the value.

If our check in step 2 passes, we just return both the indices. If we have looped through the entire array and our check in step 2 never passes, it means there's no valid answer (return []).

---

## Code for Optimal Solution

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        my_dict = {}
        for i, num in enumerate(nums):
            complement = target - num
            if complement in my_dict:
                return [my_dict[complement], i]
            else:
                my_dict[num] = i

        return []

```

---

## Complexity Analysis

- **Time Complexity:** $O(n)$ — We are iterating through nums array once, and each iteration takes up at most $O(1)$ time (lookup and insertion into a hashmap is constant time).
- **Space Complexity:** $O(n)$ — Our hashmap can contain at most n key-value pairs.

---

## Post-Mortem

N/A.
