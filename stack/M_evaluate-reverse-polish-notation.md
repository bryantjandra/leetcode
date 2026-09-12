```python
from collections import deque

# truncates toward zero means --> just chop off any decimal (can do this by converting to int())

class Solution:
    def evalRPN(self, tokens: List[str]) -> int:
        stack = deque()
        for token in tokens:
            if(self.isOperator(token)):
                right_element = stack.pop()
                left_element = stack.pop()
                res = self.evalExpression(left_element, right_element, token)
                stack.append(res)
            else:
                stack.append(int(token))
        
        return stack.pop()


    def isOperator(self, c: str) -> bool:
        if (c == "+" or c == "-" or c == "*" or c == "/"):
            return True
        return False
    
    def evalExpression(self, left_element: int, right_element: int, operand: str) -> int:
        if(operand == "+"):
            return left_element + right_element
        elif(operand == "-"):
            return left_element - right_element
        elif(operand == "*"):
            return left_element * right_element
        elif(operand == "/"):
            return int(left_element / right_element)

```