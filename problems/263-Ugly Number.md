## Problem

https://leetcode.com/problems/ugly-number/

## Solution

### Solution1

recursively

```
class Solution:
    def isUgly(self, num: int) -> bool:
        if num == 0:
            return False
        if num == 1:
            return True
        if num % 2 == 0:
            return self.isUgly(num / 2)
        if num % 3 == 0:
            return self.isUgly(num / 3)
        if num % 5 == 0:
            return self.isUgly(num / 5)
        return False
```

### Solution2

iteratively

```
class Solution:
    def isUgly(self, num: int) -> bool:
        if num == 0:
            return False
        while num % 2 == 0:
            num /= 2
        while num % 3 == 0:
            num /= 3
        while num % 5 == 0:
            num /= 5
        return num == 1
```

思路：先把num中每个因子能除的都除掉
