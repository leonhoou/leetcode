## Problem

https://leetcode.com/problems/min-stack/

## Solution

### Solution1

```
import sys

# 注意题目要求：常量时间内获取最小值
class MinStack:

    def __init__(self):
        self.l = []
        self.m = sys.maxsize
        

    def push(self, x: int) -> None:
        self.m = min(self.m, x)
        self.l.append(x)
        

    def pop(self) -> None:
        # 这里注意列表为空后，需要更新最小值为sys.maxsize
        self.l.pop()
        self.m = min(self.l) if self.l else sys.maxsize          
        

    def top(self) -> int:
        return self.l[-1]
        

    def getMin(self) -> int:
        return self.m
```


### Solution2

省略self.m 的操作：栈里存放tuple，和该解法类似，每次操作都记住最小值

```
import sys

class MinStack:

    def __init__(self):
        self.stack = []
        

    def push(self, x: int) -> None:
        self.stack.append((x, min(x, self.getMin())))
        

    def pop(self) -> None:
        self.stack.pop()     
        

    def top(self) -> int:
        if self.stack:
            return self.stack[-1][0]
        

    def getMin(self) -> int:
        if self.stack:
            return self.stack[-1][1]
        return sys.maxsize
```

### Solution3

双栈：存储元素和最小值变化过程

```
import sys

class MinStack:

    def __init__(self):
        self.stack = []
        self.m = [sys.maxsize]
        

    def push(self, x: int) -> None:
        self.stack.append(x)
        # 注意这里的等号，如果碰到相同元素怎么处理
        if x <= self.m[-1]:
            self.m.append(x)
            

    def pop(self) -> None:
        if self.stack.pop() == self.m[-1]:
            self.m.pop()
        

    def top(self) -> int:
        return self.stack[-1]
        

    def getMin(self) -> int:
        return self.m[-1]
```

### Solution4:

```
import sys

class MinStack:

    def __init__(self):
        self.stack = []
        self.m = sys.maxsize
        

    def push(self, x: int) -> None:
        if x <= self.m:
            self.stack.append(self.m)
            self.m = x
        self.stack.append(x)


    def pop(self) -> None:
        if self.stack.pop() == self.m:
            self.m = self.stack.pop()
            
        
    def top(self) -> int:
        return self.stack[-1]
        

    def getMin(self) -> int:
        return self.m
```

思想：最小值更换时，记录下这个更换过程（体现在栈里就是记录下过去最小值和当前最小值）

### Solution5:

```
class MinStack:

    def __init__(self):
        self.stack = []
        self.m = 0
        

    def push(self, x: int) -> None:
        if not self.stack:
            self.stack.append(0)
            self.m = x
        else:            
            self.stack.append(x - self.m)
            self.m = min(self.m, x)


    def pop(self) -> None:
        cur = self.stack.pop()
        if cur < 0:
            self.m = self.m - cur
            
        
    def top(self) -> int:
        if self.stack[-1] < 0:
            return self.m
        return self.stack[-1] + self.m
        

    def getMin(self) -> int:
        return self.m
```

思路：栈里存放当前值和最小值的差值，利用该方法记录每次操作时的最小值
