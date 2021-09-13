# 21. Merge Two Sorted Lists

[21. Merge Two Sorted Lists](https://leetcode.com/problems/merge-two-sorted-lists/)

### 遞迴

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def mergeTwoLists(self, l1: ListNode, l2: ListNode) -> ListNode:
        if not l1:
            return l2
        if not l2:
            return l1
        if l1.val < l2.val:
            l1.next = self.mergeTwoLists(l1.next, l2)
            return l1
        else:
            l2.next = self.mergeTwoLists(l1, l2.next)
            return l2
```

### 迭代

先建立一個 pseudo 的指針，判斷兩個列表當前的位置誰的值比較小，比較小的就加入到新的指針的列表當中，並且往下走一步。

最後要注意的是，如果有一個指針已經走完了，另一個指針可能還沒有走完，要記得在最後把那個列表給連上。這裡的解法會被用在 [148. Sort List](../sort-list.md) 。

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def mergeTwoLists(self, l1: ListNode, l2: ListNode) -> ListNode:
        prevHead = ListNode(-1)
        prev = prevHead
        while l1 and l2:
            if l1.val <= l2.val:
                prev.next = l1
                l1 = l1.next
            else:
                prev.next = l2
                l2 = l2.next
            prev = prev.next
        
        prev.next = l1 if l1 else l2
        return prevHead.next
```

如果題目給的是無序的兩個 Linked List ？那把其中一個指針連到另外一個指針上面，直接做 [148. Sort List](../sort-list.md) 就好。

