## Problem

https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/

## Solution

### Solution1

```
class Solution:
    def twoSum(self, numbers: List[int], target: int) -> List[int]:
        # two pointer
        # 双指针：快慢指针；头尾指针
        l, r = 0, len(numbers)-1
        while numbers[l] + numebrs[r] != target:
            if numbsers[l] + numbers[r] > target:
                r -= 1
            else:
                l += 1
        return [l+1, r+1]
```

思路：’查找‘可以使用双指针

### Solution2

```
class Solution:
    def twoSum(self, numbers: List[int], target: int) -> List[int]:
        # dict 
        # k: value in numbers; v: index in numbers
        dic = {}
        for i, v in enumerate(numbers):
            anum = target - numbers[i]
            if anum in dic:
                return [dic[anum], i+1]
            dic[v] = i + 1
```

思路：dict 利用数组元素值来索引其在数组中的位置

### Solution3

```
class Solution:
    def twoSum(self, numbers: List[int], target: int) -> List[int]:
        # binary search
        # to find one number's index, so need n times to find every num in numbers
        for i in range(len(numbers)):
            anum = target - numbers[i]
            l, r = i+1, len(numbers)-1
            while r >= l:
                m = (l + r) // 2
                if numbers[m] == anum:
                    return [i+1, m+1]
                elif numbers[m] > anum:
                    r = m - 1
                else:
                    l = m + 1
```

思路：’查找‘问题，使用二分查找，对数组中每一个元素都使用二分查找满足target-numbers[i]的值，时间复杂度为O(nlogn)
