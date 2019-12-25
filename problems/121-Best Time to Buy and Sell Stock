## Problem

https://leetcode.com/problems/best-time-to-buy-and-sell-stock/

## Solution

### Solution1

Dynamic-programming

```
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        ''' 空间优化前的DP
        if not prices: return 0
        l = len(prices)
        dayMaxP = [0 for _ in range(l)]
        for i in range(1, l):
            dayMaxP[i] = max(0, prices[i] - prices[i-1] + dayMaxP[i-1])
        return max(dayMaxP)
        '''
        ''' 空间优化后的DP
        l = len(prices)
        maxPrice = 0
        dayMaxP = 0
        for i in range(1, l):
            dayMaxP = max(0, prices[i] - prices[i-1] + dayMaxP) 
            maxPrice = max(maxPrice, dayMaxP)
        return maxPrice
        '''
```

### Solution2

基于对本题的理解，遍历prices的过程中，一边找到最小值，一边找到差隔最大

```
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        if not prices: return 0
        minPrice = float('inf')
        maxProfit = 0
        for price in prices:
            minPrice = min(price, minPrice)
            maxProfit = max(maxProfit, price - minPrice)
        return maxProfit
```
