## Problem

https://leetcode.com/problems/move-zeroes/

## Solution

```
class Solution:
    def moveZeroes(self, nums: List[int]) -> None:
        zero = nzero = 0
        # nzero肯定比zero跑得快        
        # nzero的作用：遍历所有的非0元素
        # 只要nzero不等于0就和zero交换位置
        while nzero < len(nums):
            if nums[nzero] != 0:
                nums[nzero], nums[zero] = nums[zero], nums[nzero]
                zero += 1
            nzero += 1
```

思路：双指针
