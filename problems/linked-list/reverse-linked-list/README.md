# 206. Reverse Linked List

[206. Reverse Linked List](https://leetcode.com/problems/reverse-linked-list/)

## 遞迴

1. 如果當前節點沒有下一個節點，有兩種情況
   1. 這個 Linked List 只有一個節點，那返回該節點就是反轉的 Linked List 
   2. 這是 Linked List 的「**最後」**一個節點，返回該節點。
2. 如果當前節點有下一個節點，繼續遞迴，遞迴返回的是最後一個節點
3. 遞迴結束，代表當前節點後面的所有節點已經反轉完畢，這時候
   1. 當前節點還是指向原先指向的節點
   2. 將當前節點原先指向的節點指向當前節點
   3. 當前節點指向 `None` 
4. 回傳結尾的節點

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def reverseList(self, head: ListNode) -> ListNode:
        if not head or not head.next: 
            return head
        last = self.reverseList(head.next)
        head.next.next = head
        head.next = None
        return last
```

## 迭代

利用兩個指針來記憶節點

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def reverseList(self, head: ListNode) -> ListNode:
        prev = None
        curr = head
        while curr:
            nxt = curr.next
            curr.next = prev
            prev = curr
            curr = nxt

        return prev
```

