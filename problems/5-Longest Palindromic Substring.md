## Problem
https://leetcode.com/problems/longest-palindromic-substring/

## Solution

**WRONG Solution:**
```
class Solution:
    def longestPalindrome(self, s: str) -> str:
        dp = [[False for j in range(len(s))] for i in range(len(s))]
        maxLen = 0
        start = -1
        for i in range(len(s)):
            for j in range(i, len(s)):
                # 子串长度小于等于2时不一定是回文子串，为啥卡在这的理解了！
                if (j - i) < 2:
                    dp[i][j] = (s[i] == s[j])
                # 子串长度大于2时动态规划
                else:
                    dp[i][j] = (dp[i+1][j-1] and (s[i] == s[j]))
                if dp[i][j] and ((j-i+1) > maxLen):
                    maxLen = j-i+1
                    start = i
        return s[start: start+maxLen]
```

DP问题的重点：从解决小问题到大问题的一个过程！！！

这是一个错误的答案：动态规划的核心就在于存储子问题的解，

思路：判断是否回文？子问题：去掉首尾元素是否回文 + 首尾元素是否相等

还有一种思路是：以数组中每一个元素为固定位置，向两边尽量拓展回文串。

这里有个常用的思路：固定首元素不行的话，考虑先固定尾元素，固定尾元素的话就是一个从小到大解决问题的路径。

**RIGHT Solution:**
```
class Solution:
    def longestPalindrome(self, s: str) -> str:
        dp = [[False for j in range(len(s))] for i in range(len(s))]
        maxLen = 0
        start = -1
        # i:start; j:end
        for j in range(len(s)):
            for i in range(j+1):
                # 子串长度小于等于2时不一定是回文子串
                if (j - i) < 2:
                    dp[i][j] = (s[i] == s[j])
                # 子串长度大于2时动态规划
                else:
                    dp[i][j] = (dp[i+1][j-1] and (s[i] == s[j]))
                if dp[i][j] and ((j-i+1) > maxLen):
                    maxLen = j-i+1
                    start = i
        return s[start: start+maxLen]
```


