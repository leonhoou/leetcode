## Problem

https://leetcode.com/problems/implement-queue-using-stacks/

## Solution

```
from collections import deque

class MyQueue:

    def __init__(self):
        self.d1 = deque()
        self.d2 = deque()
        

    def push(self, x: int) -> None:
        self.d1.append(x)
        

    def pop(self) -> int:
        if not self.d2:
            while self.d1:
                self.d2.append(self.d1.pop())
        return self.d2.pop()
    

    def peek(self) -> int:
        if not self.d2:
            while self.d1:
                self.d2.append(self.d1.pop())
        return self.d2[-1]
    

    def empty(self) -> bool:
        return (not self.d2) and (not self.d1)
```

思路：关键就是两个栈的使用，一个push元素用，一个pop元素用
