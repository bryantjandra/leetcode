```python
class Solution:
    def findMin(self, nums: list[int]) -> int:
        left, right = 0, len(nums) - 1
        while left < right:
            mid = (left + right) // 2
            if nums[mid] < nums[right]:
                right = mid # we keep mid because mid itself might be the minimum (all the elements less than or equal to mid, have a change of being the minimum)
            elif nums[mid] > nums[right]:
                left = mid + 1
        
        return nums[left]


# intuition: a rotated sorted array has two halves: the lesser half and the greater halves. 

# whenever mid is greater than the rightmost element, mid is definitely at the greater half, which would mean the minimum element is definitely after mid. so we set left = mid + 1 and continue binary search.

# whenever mid is less than the rightmost element, mid is definitely at the lesser half, thus mid and any element before mid COULD be the minimum element, so we set right=mid (in order to include mid to be a potential answer for the minimum element). 

# whenever left == right, this would mean the window has shrank to the point where the element at left/right is at the start of the lesser half, and the element at left/right is the minimum element.
```