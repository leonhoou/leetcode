## Problem
https://leetcode.com/problems/longest-palindromic-substring/

## Solution

**WRONG Solution:**
```
class Solution:
    def longestPalindrome(self, s: str) -> str:
        dp = [[False for j in range(len(s))] for i in range(len(s))]
        maxLen = 0
        for i in range(len(s)):
            for j in range(i, len(s)):
                # 子串长度小于等于2时一定是回文子串
                if (j - i) < 2:
                    dp[i][j] = True
                # 子串长度大于2时动态规划
                else:
                    dp[i][j] = (dp[i+1][j-1] and (s[i] == s[j]))
                if dp[i][j] and ((j-i+1) > maxLen):
                    maxLen = j-i+1
                    start = i
        return s[start: start+maxLen]
```
这是一个错误的答案：动态规划的核心就在于存储子问题的解，

该答案利用的是len(s)*len(s)的二维数组的上三角部分，且先固定起始位置i，再由j遍历s，
这就导致了会判断长度大于2的子串是否是回文的，但是上三角>i部分的子问题解还没判断，这就导致子问题解没有存储。

应该利用下三角部分，且先固定结束位置j，再由i遍历s之间位置的元素

**RIGHT Solution:**
```
class Solution:
    def longestPalindrome(self, s: str) -> str:
        dp = [[False for j in range(len(s))] for i in range(len(s))]
        maxLen = 0
        # i:start; j:end
        for j in range(len(s)):
            for i in range(j+1):
                # 子串长度小于等于2时一定是回文子串
                if (j - i) < 2:
                    dp[i][j] = True
                # 子串长度大于2时动态规划
                else:
                    dp[i][j] = (dp[i+1][j-1] and (s[i] == s[j]))
                if dp[i][j] and ((j-i+1) > maxLen):
                    maxLen = j-i+1
                    start = i
        return s[start: start+maxLen]
```


