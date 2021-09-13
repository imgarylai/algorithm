# 876. Middle of the Linked List

[876. Middle of the Linked List](https://leetcode.com/problems/middle-of-the-linked-list/)

快慢指針

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def middleNode(self, head: ListNode) -> ListNode:
        slow = head
        fast = head
        
        while fast and fast.next:
            slow = slow.next
            fast = fast.next.next
            
        return slow
```

