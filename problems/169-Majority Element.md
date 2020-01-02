## Problem

https://leetcode.com/problems/majority-element/

## Solution

### Solution1

```
class Solution:
    def majorityElement(self, nums: List[int]) -> int:
        # dict
        dic = {}
        for num in nums:
            dic[num] = dic.get(num, 0) + 1
            if dic[num] > (len(nums) // 2):
                return num
```

思路：利用dict存放(value, num)

### Solution2

```
class Solution:
    def majorityElement(self, nums: List[int]) -> int:
        # majority数量超过一半，相当于是让该元素的一半把其他的都抵消了，反正还有剩余，那最多的肯定就是他啦
        # 注意：这个数量一定要超过一半哦
        maj = nums[0]
        counter = 1
        for i in range(1, len(nums)):
            if nums[i] == maj:
                counter += 1
            else:
                if counter > 0:
                    counter -= 1
                else:
                    maj = nums[i]
                    counter = 1
        return maj
```

化简：

```
class Solution:
    def majorityElement(self, nums: List[int]) -> int:
        maj = 0
        cnt = 0
        for num in nums:
            if cnt == 0:
                maj = num
            if num == maj:
                cnt += 1
            else:
                cnt -= 1
        return maj
```

思路：利用数量最多的元素的数量超过一半这个特性

### Solution3

```
class Solution:
    def majorityElement(self, nums: List[int]) -> int:
        # DC
        if len(nums) == 1:
            return nums[0]
        a = self.majorityElement(nums[:len(nums)//2])
        b = self.majorityElement(nums[len(nums)//2:])
        return [b, a][nums.count(a) > nums.count(b)]
 ```
 
 思路：分治的想法可以这样：找到终止条件；获取每个子问题的解；直接对该解进行最终结果的处理。（不用额外考虑递归的详细处理）
