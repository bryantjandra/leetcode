```python
class Solution:
    def searchMatrix(self, matrix: list[list[int]], target: int) -> bool:
        left = 0
        right = len(matrix) - 1
        while left <= right:
            mid = int((left + right) / 2)
            candidate_row = matrix[mid]


            if (target >= candidate_row[0] and target <= candidate_row[-1]):
                # run binary search within this row, if cant find the element then return false
                row_left = 0
                row_right = len(candidate_row) - 1
                while row_left <= row_right:
                    row_mid = int((row_left + row_right) / 2)
                    if candidate_row[row_mid] == target:
                        return True
                    elif candidate_row[row_mid] < target:
                        row_left = row_mid + 1
                    elif candidate_row[row_mid] > target:
                        row_right = row_mid - 1
                return False



            elif (target >= candidate_row[-1]):
                left = mid + 1
            elif (target <= candidate_row[0]):
                right = mid - 1
        

        return False
```

## Notes:

- Time complexity will be O(log m) for the outer binary search loop, and then we do binary search on one row which will take O(log n). This will mean O(log m + log n) time complexity or O(log (m*n)). 