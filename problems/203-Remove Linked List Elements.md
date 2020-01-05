## Problem

https://leetcode.com/problems/remove-linked-list-elements/

## Solution

### Solution1

```
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def removeElements(self, head: ListNode, val: int) -> ListNode:
        if not head:
            return None
        h = ListNode(-1)
        h.next = head
        p = h
        
        while p.next:
            if p.next.val == val:
                p.next = p.next.next
            else:
                p = p.next
        return h.next
```

思路：链表的基本操作，有设置虚拟头结点的想法就可。

### Solution2

```
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def removeElements(self, head: ListNode, val: int) -> ListNode:
        if not head:
            return None
        head.next = self.removeElements(head.next, val)
        head = head.next if head.val == val else head
        return head
```

思路：分治（递归）！！！要培养这个想法！！！
