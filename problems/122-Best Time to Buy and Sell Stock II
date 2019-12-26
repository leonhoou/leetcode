## Problem

https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii/

## Solution

```
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        posP = [prices[i] - prices[i-1] for i in range(1, len(prices)) if prices[i] - prices[i-1] > 0]
        return sum(posP)
```

### Tips

有些算法题不用使用传统的数据结构、算法之类的，重点是了解题目的意思，本题可以画图理解。
