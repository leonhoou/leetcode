## Problem

https://leetcode.com/problems/valid-palindrome/

## Solution

```
import re

class Solution:
    def isPalindrome(self, s: str) -> bool:
        return re.sub(r'\W', '', s).lower() == re.sub(r'\W', '', s).lower()[::-1]
```

### Tips

学会Python的re使用（正则表达式）和字符串的反转

```
class Solution:
    def isPalindrome(self, s: str) -> bool:
        s = ''.join([e for e in s if e.isalnum()]).lower()
        return s == s[::-1]
```

### Tips

Python一定要会列表生成式的使用方法

···
class Solution:
    def isPalindrome(self, s: str) -> bool:
        if not s: return True
        # 双指针
        head = 0
        tail = len(s) - 1
        while tail > head:
            # 这里我本来使用的是while循环，更改为if和continue的使用，continue终止本次循环可以直接判断条件，条件不成立可以直接跳出外层while循环
            '''
            while not s[tail].isalnum() and tail > head:
                ...
            '''
            if not s[tail].isalnum():
                tail -= 1
                continue
            if not s[head].isalnum():
                head += 1
                continue
            if s[head].lower() == s[tail].lower():
                head += 1
                tail -= 1
            else:
                return False
        return True
···

## Tips

回文类型的题注意使用双指针解决
