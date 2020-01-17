## Problem

https://leetcode.com/problems/sum-of-two-integers/

## Solution

```
class Solution:
    def getSum(self, a: int, b: int) -> int:
        '''
        存在的问题是：-1与1，因为python是infinite number of bit
        '''
        while b:
            # 获取需要进位的位置
            carry = a & b
            # 不考虑进位的计算
            a = a ^ b
            # 进位需要左移一位
            # 进位左移后需要与不考虑进位的结果继续XOR，直到没有进位
            b = carry << 1
        return a
```

注：python位运算是infinite的，所以有限制
