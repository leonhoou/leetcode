## Problem

https://leetcode.com/problems/merge-sorted-array/

## Solution

### Python

```
class Solution:
    def merge(self, nums1: List[int], m: int, nums2: List[int], n: int) -> None:
        """
        Do not return anything, modify nums1 in-place instead.
        """
        # 从后往前看：最后一个元素都是最大值
        # 注意：条件一定要考虑所有情况
        # m可以先结束；n也可以先结束
        # m先结束：nums2的前n个元素放到nums1的前n个元素中
        # n先结束：pass
        while m > 0 and n > 0:
            if nums1[m-1] >= nums2[n-1]:
                nums1[m+n-1] = nums1[m-1]
                m -= 1
            else:
                nums1[m+n-1] = nums2[n-1]
                n -= 1
        if n > 0:
            nums1[:n] = nums2[:n]
```

## Tips

Note1: 归并排序的merge操作，前提是空间复杂度为O(1)，从后往前（两个数组中的最后元素决定当前nums1中的最大元素，所以决定的就是nums1的最后位置的元素）

Note2：使用判断语句时，一定要注意所有的判断条件，慎重！！！
