## Problem

https://leetcode.com/problems/reverse-bits/

## Solution

```
class Solution:
    def reverseBits(self, n: int) -> int:
        res = 0
        for _ in range(32):
            # n&1 取n的最后一位
            res = (res << 1) + (n & 1)
            n >>= 1
        return res
```
