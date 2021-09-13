# 141. Linked List Cycle

[141. Linked List Cycle](https://leetcode.com/problems/linked-list-cycle/)

這個題目是利用雙指針來找一個 `Linked List` 有沒有環，概念就是我們有兩個人在賽跑，一個人跑得快，一個人跑得慢，如果說這是一個直行的跑道，那快的人就會直接到終點，也就代表沒有環。

但如果有環的話，那這樣跑得快的人遲早會追上慢的人。當追上了就代表有環了。

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def hasCycle(self, head: ListNode) -> bool:
        fast = head
        slow = head

        while fast and fast.next:
            fast = fast.next.next
            slow = slow.next
            if fast == slow:
                return True

        return False
```

