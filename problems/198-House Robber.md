## Problem

https://leetcode.com/problems/house-robber/

## Solution

```
class Solution:
    def rob(self, nums: List[int]) -> int:
        if not nums:
            return 0
        cur = 0
        prev1 = 0
        prev2 = 0
        for num in nums:
            cur = max(prev2 + num, prev1)
            prev2 = prev1
            prev1 = cur
        return cur
```

分享：

https://leetcode.com/problems/house-robber/discuss/156523/From-good-to-great.-How-to-approach-most-of-DP-problems.

这是一个对DP和每一步优化的非常好的解释！！！
