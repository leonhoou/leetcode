## Problem

https://leetcode.com/problems/single-number/

## Solution

```
import functools

class Solution:
    def singleNumber(self, nums: List[int]) -> int:
        
        ''' python用value获取key的方法啊！！！
        # 傻子方法：list(d.keys())[list(d.values()).index(1)]
        d = {}
        for num in nums:
            d[num] = d.get(num, 0) + 1
        for k, v in d.items():
            if v == 1:
                return k'''
        
        ''' 异或思路：与本身为0，与0为本身
        # 要有位运算的感觉
        v = 0
        for num in nums:
            v ^= num
        return v
        '''
        
        ''' 能想到set之后元素翻倍出现，怎么没想到求和呢！！！
        return sum(set(nums))*2 - sum(nums)
        '''
        
        # return functools.reduce(lambda x, y: x ^ y, nums)
    
        return functools.reduce(operator.xor, nums)
```
