# 369. Plus One Linked List

[369. Plus One Linked List](https://leetcode.com/problems/plus-one-linked-list/)

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def plusOne(self, head: ListNode) -> ListNode:
        tmp = ListNode()
        tmp.next = head
        not_nine = tmp

        while head:
            if head.val != 9:
                not_nine = head
            head = head.next

        not_nine.val += 1
        not_nine = not_nine.next

        while not_nine:
            not_nine.val = 0
            not_nine = not_nine.next

        return tmp if tmp.val else tmp.next
```
