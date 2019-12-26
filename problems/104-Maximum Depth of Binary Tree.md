## Problem

https://leetcode.com/problems/maximum-depth-of-binary-tree/description/

## Solution

### Solution1:

```
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None
from collections import deque
class Solution:
    # 广度优先遍历
    # 特点：会把每一层的节点都加到队列中
    def maxDepth(self, root: TreeNode) -> int:
        if not root:
            return 0
        depth = 0
        d = deque()
        d.append(root)
        while d:
            depth += 1
            # 遍历每一层的节点
            for _ in range(len(d)):
                e = d.popleft()
                if e.left:
                    d.append(e.left)
                if e.right:
                    d.append(e.right)
        return depth
```

### Solution2:

```
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None
class Solution:
    '''
    # 深度优先遍历：递归
    # 时间复杂度：节点数
    def maxDepth(self, root: TreeNode) -> int:
        if not root:
            return 0       
        return max(self.maxDepth(root.left), self.maxDepth(root.right)) + 1
    '''
    
```
