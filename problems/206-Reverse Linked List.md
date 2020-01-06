## Problem

https://leetcode.com/problems/reverse-linked-list/

## Solution

### Solution1

```
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def reverseList(self, head: ListNode) -> ListNode:
        # 这应该是分治吧（大问题转为小问题）
        if not head or not head.next:
            return head     
        h = self.reverseList(head.next)
        if head.next:
            head.next.next = head
        head.next = None
        return h
```

### Solution2

```
class Solution:
    def reverseList(self, head: ListNode) -> ListNode:
        '''if not head:
            return None
        newHead = head.next
        head.next = None        
        while newHead:
            n = newHead.next
            newHead.next = head
            head = newHead
            newHead = n            
        return head'''
    
        # 改进
        newHead = None
        while head:
            n = head.next
            head.next = newHead
            newHead = head
            head = n            
        return newHead
```

### Solution3

```
class Solution:
    def reverseList(self, head: ListNode) -> ListNode:    
        # 发现head和newHead一直重复，所以延伸出来递归
        return self.reverse(head, None)
    
    def reverse(self, head: ListNode, newHead: ListNode) -> ListNode:
        if not head:
            return newHead
        n = head.next
        head.next = newHead
        return self.reverse(n, head)
```
