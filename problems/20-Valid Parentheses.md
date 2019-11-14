## problem:
https://leetcode.com/problems/valid-parentheses/
  
## solution:
python code:

```python3
class Solution:
    def isValid(self, s: str) -> bool:
        openBracketStack = []
        brackets = {'(': ')', '{': '}', '[': ']'}
        for e in s:
            if e in brackets.keys():
                openBracketStack.append(e)
            else:
                if len(openBracketStack) == 0:
                    return False
                top = openBracketStack.pop()
                if e != brackets.get(top):
                    return False
        if len(openBracketStack) != 0:
            return False
        return True
```

## skill
```python3
class Solution:
    def isValid(self, s: str) -> bool:
        openBracketStack = []
        brackets = {'(': ')', '{': '}', '[': ']'}
        for e in s:
            if e in brackets.keys():
                openBracketStack.append(e)
            else:
                # if len(openBracketStack) == 0:
                # 空列表在if条件中就是False
                if not openBracketStack:
                    return False
                top = openBracketStack.pop()
                if e != brackets.get(top):
                    return False
        # if len(openBracketStack) != 0:
        #     return False
        # return True
        # 列表是否为空可以获取False/True
        return (not openBracketStack)
```
