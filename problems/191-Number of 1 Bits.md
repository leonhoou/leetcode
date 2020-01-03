## Problem

https://leetcode.com/problems/number-of-1-bits/

## Solution

### Solution1

bit manipulation

```
class Solution:
    def hammingWeight(self, n: int) -> int:
        res = 0
        for _ in range(32):
            res += (n & 1)
            n >>= 1
        return res
```


### Solution2

```
class Solution:
    def hammingWeight(self, n: int) -> int:    
        res = 0
        while n:
            # n & (n - 1) 消除n从右向左碰到的第一个1，总共消除几次，说明n就有几个1
            n = n & (n - 1)
            res += 1
        return res
```

一个trick
