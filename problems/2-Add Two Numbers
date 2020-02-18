## Problem

https://leetcode.com/problems/add-two-numbers/

## Solution

```
class Solution:
    def addTwoNumbers(self, l1: ListNode, l2: ListNode) -> ListNode:
        bit = 0
        head = ListNode(-1)
        curNode = head
        while l1 or l2 or bit:
            sum = 0
            if l1:
                sum += l1.val
                l1 = l1.next
            if l2:
                sum += l2.val
                l2 = l2.next
            sum += bit
            bit = sum // 10
            node = ListNode(sum % 10)
            curNode.next = node
            curNode = node
        return head.next
```

有个解法，惊叹！

https://leetcode.com/problems/add-two-numbers/discuss/1102/Python-for-the-win
