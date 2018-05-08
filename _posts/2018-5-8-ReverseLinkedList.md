---
layout: post
title: Reverse Linked List in Two Ways
---

A linked list can be reversed either iteratively or recursively. Could you implement both?

### Iteratively

```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def reverseList(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        if head == None:
            return head
        
        prev = None
        cur = head
        nt = head.next
        
        while cur:
            cur.next = prev
            prev = cur
            cur = nt
            if nt:
                nt = nt.next
        return prev
```

### Recursively

```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def reverseList(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        if head == None:
            return head
        if head.next == None:
            new_head = head
        else:
            new_head = self.reverseList(head.next)
            head.next.next = head
            head.next = None
        return new_head
```
