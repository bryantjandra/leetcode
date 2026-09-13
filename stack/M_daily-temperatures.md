```python
from collections import deque
class Solution:
    def dailyTemperatures(self, temperatures: List[int]) -> List[int]:
        res = [0] * len(temperatures)
        stack = deque()
        for idx, temp in enumerate(temperatures):
            while (len(stack) > 0 and (stack[-1])[0] < temp):
                top_temp = stack.pop()
                res[top_temp[1]] = idx - top_temp[1]
            stack.append((temp, idx))
        
        return res

```

## Note:

- A monotonically decreasing stack is used to find the next largest element here. This type of stack ensures that the elements from the bottom to the top of the stack, are in decreasing order. 

- Thus, whenever we encounter an element that is greater than the element at the top of the stack, we will keep popping from the stack until it is valid (current element is less than the top of the stack element).