## Problem

https://leetcode.com/problems/median-of-two-sorted-arrays/

## Solution

```
class Solution:
    def findMedianSortedArrays(self, nums1: List[int], nums2: List[int]) -> float:
        # 中位数：一个数组，找到对半分；两个数组，找到对半分的分界线。
        # 两个排序数组：左半部分left都是小的，右半部分都是大的，找到分界线即可。
        '''
            left  | right
         a  1 2 6 / 7 8  分割位置j
         b  3 4 / 5 9    分割位置i（注：i是短数组的切割点）
            i+j=m-i+n-j or m-i+n-j+1 -> j = (m+n+1)//2-i
            要满足：b[i-1]<=a[j] and a[j-1]<=b[i]
        '''
        m, n = len(nums1), len(nums2)
        if m > n:
            m, n = n, m
            nums1, nums2 = nums2, nums1
        # i和j都是有m+1[0-m], n+1[0-n]个位置的
        l, r = 0, m
        # 这里可以使用binary search找i的位置
        while  l <= r:
            i = (l + r) // 2
            j = (m + n + 1) // 2 - i
            if i > 0 and nums1[i-1] > nums2[j]:
                r = i - 1
            elif i < m and nums1[i] < nums2[j-1]:
                l = i + 1
            else:
                # 考虑边界值(在结果maxL和maxR的维度上考虑)
                if i == 0:
                    maxL = nums2[j-1]
                elif j == 0:
                    maxL = nums1[i-1]
                else:
                    maxL = max(nums1[i-1], nums2[j-1])
                if (m+n) % 2:
                    return maxL
                if i == m:
                    minR = nums2[j]
                elif j == n:
                    minR = nums1[i]
                else:
                    minR = min(nums1[i], nums2[j])
                return (maxL + minR) / 2
        return None
            
```
