## Problem

https://leetcode.com/problems/contains-duplicate-ii/

## Solution

### Solution1

```
class Solution:
    def containsNearbyDuplicate(self, nums: List[int], k: int) -> bool:
        dic = {}
        for i in range(len(nums)):
            if nums[i] in dic:
                if (i - dic[nums[i]]) <= k:
                    return True
            dic[nums[i]] = i
        return False
```

### Solution2

```
class Solution:
    def containsNearbyDuplicate(self, nums: List[int], k: int) -> bool:
        s = set()
        for i, v in enumerate(nums):
            if i > k:
                s.remove(nums[i-k-1])
            if v in s:
                return True
            s.add(v)
        return False
```

思路：利用set维护一个判断是否有重复元素的窗口
