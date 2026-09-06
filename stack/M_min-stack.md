```python
from collections import deque

class MinStack:

    def __init__(self):
        # stack one's top will always hold the minimum value
        self.stack_one = deque()

        # stack two is our ground truth stack
        self.stack_two = deque()

    def push(self, value: int) -> None:
        self.stack_two.append(value)

        if len(self.stack_one) == 0:
            self.stack_one.append(value)
            return
        
        if(value <= self.stack_one[-1]):
            self.stack_one.append(value)

    def pop(self) -> None:
        popped_value = self.stack_two.pop()
        if popped_value == self.stack_one[-1]:
            self.stack_one.pop()
        

    def top(self) -> int:
        return self.stack_two[-1]
        

    def getMin(self) -> int:
        return self.stack_one[-1]


# Your MinStack object will be instantiated and called as such:
# obj = MinStack()
# obj.push(value)
# obj.pop()
# param_3 = obj.top()
# param_4 = obj.getMin()

```