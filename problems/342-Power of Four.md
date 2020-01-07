## Problem

https://leetcode.com/problems/power-of-four/

## Solution

```
class Solution:
    def isPowerOfFour(self, num: int) -> bool:
        return (num > 0) and (num & (num-1) == 0) and (num & 0x55555555 == num)
```

思路：主要就是有bit manipulation的感觉，个人感觉解法太局限于本题了（0x55555555）
