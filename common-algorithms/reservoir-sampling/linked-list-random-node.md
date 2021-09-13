# 382. Linked List Random Node

[382. Linked List Random Node](https://leetcode.com/problems/linked-list-random-node/)

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:

    def __init__(self, head: Optional[ListNode]):
        """
        @param head The linked list's head.
        Note that the head is guaranteed to be not null, so it contains at least one node.
        """
        self.head = head

    def getRandom(self) -> int:
        """
        Returns a random node's value.
        """
        scope = 1
        res = 0
        curr = self.head
        while curr:
            # decide whether to include the element in reservoir
            if random.random() < 1 / scope:
                res = curr.val
            # move on to the next node
            curr = curr.next
            scope += 1
        return res
        
# Your Solution object will be instantiated and called as such:
# obj = Solution(head)
# param_1 = obj.getRandom()
```

