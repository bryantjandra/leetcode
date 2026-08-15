```python
class Solution:
    def threeSum(self, nums: list[int]) -> list[list[int]]:
        res = []
        nums.sort()
        for i in range(0, len(nums) - 2):
            if(i > 0 and nums[i] == nums[i-1]):
                continue
            target = 0 - nums[i]
            left = i + 1
            right = len(nums) - 1
            while left < right:
                currSum = nums[left] + nums[right]
                if currSum == target:
                    res.append([nums[left], nums[right], nums[i]])
                    left += 1
                    right -= 1
                    while left < right and nums[left] == nums[left-1]:
                        left += 1
                    while left < right and nums[right] == nums[right+1]:
                        right -= 1
                elif currSum < target:
                    left += 1
                elif currSum > target:
                    right -= 1
        
        return res
# [-4,-1,-1,0,1,2]
# target = 0 - (-1) = 4
```


## Notes

