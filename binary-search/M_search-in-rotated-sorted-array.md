```python
class Solution:
    def search(self, nums: list[int], target: int) -> int:
        # finding the index of the minimum element in a rotated sorted array
        left, right = 0, len(nums) - 1
        while left < right:
            mid = (left + right) // 2
            if nums[mid] > nums[right]:
                left = mid + 1
            elif nums[mid] < nums[right]:
                right = mid
        
        min_index = left

        binary_search_smaller_array = self.binarySearch(nums, target, min_index, len(nums) - 1)
        binary_search_greater_array = self.binarySearch(nums, target, 0, min_index - 1)

        if binary_search_smaller_array != -1:
            return binary_search_smaller_array
        
        return binary_search_greater_array


    def binarySearch(self, nums: list[int], target: int, left: int, right: int) -> int:
        while left <= right:
            mid = (left + right) // 2
            if nums[mid] == target:
                return mid
            elif nums[mid] < target:
                left = mid + 1
            elif nums[mid] > target:
                right = mid - 1
        
        return -1

            

# 6,7,0,1,2,4,5
```