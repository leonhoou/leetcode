## Problem

https://leetcode.com/problems/path-sum-iii/

## Solution

```
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None
from typing import Dict

# 深度优先搜索
class Solution:
    def pathSum(self, root: TreeNode, sum: int) -> int:
        '''
        思路：
            root->curnode 保存了prefixsum
            target表示的是somenode->curnode，
            target = root->curnode的curSum - root->somenode的curSum
            这是最重要的一点，理解这一点，题就容易了
        '''
        # 这里有个点是如何global res
        self.res = 0
        # store root to each node's SUM
        # key: SUM, value: TIMES
        # 这里的0:1很关键
        dic = {0:1}
        # curSum: root-curNode's SUM
        self.path(root, sum, dic, 0)
        return self.res
        
    def path(self, node: TreeNode, sum: int, dic: Dict, curSum: int) -> int:
        if node:
            curSum += node.val
            self.res += dic.get(curSum - sum, 0)
            dic[curSum] = dic.get(curSum, 0) + 1        
            self.path(node.left, sum, dic, curSum)
            self.path(node.right, sum, dic, curSum)
            # 注意这里root和left和right都遍历完了，应该换root的neighbor节点了，所以到root的curSum应该-1
            dic[curSum] -= 1
```

思路：路径上连续值求和，可以使用初始点到终点的和减去初始点到路径上任一点的和
