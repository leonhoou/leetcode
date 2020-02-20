## Problem

https://leetcode.com/problems/unique-paths/

## Solution

```
class Solution:
    def uniquePaths(self, m: int, n: int) -> int:
        '''dp = [[1 for _ in range(n)] for _ in range(m)]
        # 必有一条路径，所以初始化可都为1
        # for i in range(n):
        #     dp[0][i] = 1
        # for i in range(m):
        #     dp[i][0] = 1
        for i in range(1, m):
            for j in range(1, n):
                dp[i][j] = dp[i-1][j] + dp[i][j-1]
        return dp[m-1][n-1]'''
        # dp[i][j]更新的时候只利用到了上一行的数据
        dp = [1] * n
        for i in range(1, m):
            for j in range(1, n):
                dp[j] = dp[j-1] + dp[j]
        return dp[-1]
```

Tips：

二维动态规划可以优化空间到一行，因为二维数组的每次更新只用到上一行的数据
