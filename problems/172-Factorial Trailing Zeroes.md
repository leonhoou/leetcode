## Problem

https://leetcode.com/problems/factorial-trailing-zeroes/

## Solution

```
class Solution:
    def trailingZeroes(self, n: int) -> int:
        '''# 递归
        if n < 5: 
            return 0
        return n // 5 + self.trailingZeroes(n // 5)'''
        # 非递归
        r = 0
        while n >= 5:
            n //= 5
            r += n
        return r
```

思路：就是计算n里面有多少个5，注意：25,125...里面有不止一个5
