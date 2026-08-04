```python
class Solution:
    def longestConsecutive(self, nums: List[int]) -> int:
        mySet = set()
        for num in nums:
            mySet.add(num)
        

        lengthLongest = 0

        for num in nums:
            if (num - 1) in mySet:
                continue
            else:
                currLength = 1
                currNum = num
                while (currNum + 1) in mySet:
                    currNum += 1
                    currLength += 1
                
                lengthLongest = max(lengthLongest, currLength)
                
                if lengthLongest > (len(nums) / 2):
                    return lengthLongest
        

        return lengthLongest
```