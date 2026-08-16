```python
class Solution:
    def maxArea(self, height: List[int]) -> int:
        left, right = 0, len(height) - 1
        maxArea = 0
        while left < right:
            currArea = (right - left) * min(height[left], height[right])
            maxArea = max(maxArea, currArea)
            if height[left] < height[right]:
                left += 1
            elif height[left] >= height[right]:
                right -= 1
        
        return maxArea
```