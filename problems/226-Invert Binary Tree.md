## Problem

https://leetcode.com/problems/invert-binary-tree/

## Solution

## Solution1

BFS

```
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None
from collections import deque

class Solution:
    def invertTree(self, root: TreeNode) -> TreeNode:
        if not root:
            return None
        deq = deque()
        deq.append(root)
        
        while deq:
            front = deq.popleft()
            '''
            tmp = front.left
            front.left = front.right
            front.right = tmp
            '''
            # 偷学一手
            front.left, front.right = front.right, front.left
            if front.left:
                deq.append(front.left)
            if front.right:
                deq.append(front.right)
        return root
```

化简：

```
from collections import deque

class Solution:
    def invertTree(self, root: TreeNode) -> TreeNode:
        deq = deque([root])        
        while deq:
            front = deq.popleft()
            if front:
                front.left, front.right = front.right, front.left
                deq.extend([front.left, front.right])
        return root
```

### Solution2

```
class Solution:
    def invertTree(self, root: TreeNode) -> TreeNode:
        if not root:
            return None
        left = self.invertTree(root.left)
        right = self.invertTree(root.right)        
        if left or right:
            tmp = left
            root.left = right
            root.right = tmp            
        return root
```

### Solution3

```
class Solution:
    def invertTree(self, root: TreeNode) -> TreeNode:
        if not root:
            return None
        '''
        stack = []
        stack.append(root)
        '''
        stack = [root]
        
        while stack:
            top = stack.pop()            
            top.left, top.right = top.right, top.left              
            if top.right:
                stack.append(top.right)
            if top.left:
                stack.append(top.left)
        return root
```
