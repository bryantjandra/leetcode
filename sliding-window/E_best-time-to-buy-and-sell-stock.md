```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        highestProfit = 0
        left = 0
        for right in range(1, len(prices)):
            if prices[right] < prices[left]:
                left = right
            else:
                highestProfit = max(highestProfit, prices[right] - prices[left])

        return highestProfit
```