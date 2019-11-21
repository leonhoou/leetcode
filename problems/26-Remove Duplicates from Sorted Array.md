## Problem:
https://leetcode.com/problems/remove-duplicates-from-sorted-array/

## Solutions:
```
class Solution:
    def removeDuplicates(self, nums: List[int]) -> int:
        if nums:
            slow = 0
            for fast in range(0, len(nums)):
                if nums[slow] != nums[fast]:
                    slow += 1
                    nums[slow] = nums[fast]
            return slow + 1
        return 0
```

## Tips:
快指针和慢指针：

慢指针：用来确定结果数组的每一个位置的元素

快指针：用来遍历初始数组的每一个元素

**注意哦：**

for循环中隐含快指针+1的操作了，所以循环体内不要快指针+1的代码
