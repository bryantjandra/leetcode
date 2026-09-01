```python
from collections import deque

class Solution:
    def isValid(self, s: str) -> bool:
        stack = deque()
        for c in s:
            if (c == '(' or c == '{' or c == '['):
                stack.append(c)
            else:
                if len(stack) == 0:
                    return False
                else:
                    curr_bracket = stack.pop()
                    if curr_bracket == '(' and c != ')':
                        return False
                    elif curr_bracket == '{' and c != '}':
                        return False
                    elif curr_bracket == '[' and c != ']':
                        return False
                        
        if len(stack) != 0:
            return False

            
        return True
```

## NOTE:

- Use `from collections import deque` to instantiate stacks in Python.