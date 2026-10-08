```python
import math

class Solution:
    def minEatingSpeed(self, piles: list[int], h: int) -> int:
        most_bananas = 0 # holds the amount of bananas in the largest pile. this starts as our baseline as it is virtually impossible for Koko to eat n piles with n-1 speed. 
        for pile in piles:
            most_bananas = max(most_bananas, pile)
        
        left, right = 1, most_bananas # we cannot eat bananas with a speed of 0, so left starts as 1
        min_k = most_bananas

        while left <= right:
            mid = (left + right) // 2
            hours_needed = self.calculateHoursNeeded(mid, piles)
            if hours_needed <= h:
                min_k = min(min_k, mid)
                right = mid - 1
            elif hours_needed > h:
                left = mid + 1
        
        return min_k


    def calculateHoursNeeded(self, speed: int, piles: list[int]) -> int:
        hours = 0
        for pile in piles:
            hours = hours + math.ceil(pile/speed)
        return hours
```

# Note:

- Time complexity analysis: 
    1. $O(n)$ from iterating through the piles array once. 
    2. $O((log m)* n)$ from doing binary search on the largest pile (log m) and in each iteration we need to calculate the hours needed (n). 
    3. Thus, $O(n)$ + $O((log m)* n)$ = $O(n log m)$. 




