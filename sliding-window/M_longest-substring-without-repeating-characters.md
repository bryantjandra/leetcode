```python
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        mySet = set()
        longestLength = 0
        left = 0
        for right in range(0, len(s)):
            while s[right] in mySet:
                mySet.remove(s[left])
                left += 1
            mySet.add(s[right])
            longestLength = max(longestLength, right - left + 1)
        
        return longestLength
```

## NOTE:

- The time complexity stays at $O(n)$. Yes, there is an inner while loop, but because `left` only moves forward and it never resets, the overall time complexity stays at $O(n)$. Across the entire loop, `left` advances at most `n` times total. Thus, `right` moves `n` times, and `left` moves at most `n` times --> $O(n)$ and not $O(n^2)$. 