## Problem

https://leetcode.com/problems/maximum-subarray/

## Solution

### Solution1

动态规划

```
class Solution:
    def maxSubArray(self, nums: List[int]) -> int:        
        l = len(nums)
        dp = [nums[0] for i in range(l)]
        for i in range(1, l):
            dp[i] = max(dp[i-1]+nums[i], nums[i])
        return max(dp)
```

### Solution2

动态规划（节省空间）

```
class Solution:
    def maxSubArray(self, nums: List[int]) -> int:
        l = len(nums)
        curMax = nums[0]
        gloMax = nums[0]
        for i in range(1, l):
            curMax = max(curMax+nums[i], nums[i])
            gloMax = max(gloMax, curMax)
        return gloMax
```

### Solution3

分治思想

```
import sys
class Solution:
    def maxSubArray(self, nums: List[int]) -> int:        
        return self.maxVal(nums, 0, len(nums)-1) 
        
    def maxVal(self, nums: List[int], l: int, r: int) -> int:
        if l > r:
            return -sys.maxsize
        
        m = (l + r) // 2
        lMax = self.maxVal(nums, l, m-1)
        rMax = self.maxVal(nums, m+1, r)

        curSum = 0
        # 0 的原因：只要左/右序列的前缀和大于0即可使用；都不大于0就不适用这两个序列，所以+0
        lMaxSum = rMaxSum = 0
        # reversed() 返回一个反转的迭代器
        for i in reversed(range(l, m)):
            curSum += nums[i]
            lMaxSum = max(lMaxSum, curSum)
        # 注意清空curSum的值
        curSum = 0
        for i in range(m+1, r+1):
            curSum += nums[i]
            rMaxSum = max(rMaxSum, curSum)
        mMax = lMaxSum + rMaxSum + nums[m]
        return max(lMax, mMax, rMax)
```

## tips

概念：前缀和；后缀和；分治，递归；动态规划
