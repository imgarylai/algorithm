# 19. Remove Nth Node From End of List

[19. Remove Nth Node From End of List](https://leetcode.com/problems/remove-nth-node-from-end-of-list/)

這一題我的第一個想法是我先走一趟算出整個 `Linked List` 有多長，接著我把所有的長度減去 `n` ，這就代表我需要從起點往下走幾步。

不過此時我們需要借助一個虛擬節點，虛擬節點的下一個點才是起點，並且從虛擬起點開始往下走，直到走到了要被刪除的點的前一個點，這時候我們就把需要刪除的節點刪掉。

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def removeNthFromEnd(self, head: ListNode, n: int) -> ListNode:
        if not head:
            return None
        l = 0
        curr = head
        while curr:
            l += 1
            curr = curr.next
        l -= n 
        # tihs is important because sometimes the expected remove node is the head node. 
        dummy = ListNode(-1)
        dummy.next = head
        curr = dummy
        while l > 0:
            l -= 1
            curr = curr.next
        
        curr.next = curr.next.next    
        return dummy.next
```

這一題也可以用快慢指針的方式來處理

首先我們先將快指針走 `n` 步，如果說快指針為空了，那代表需要被刪除的節點就是一開始的起點。接著快慢指針一起走，走到快指針走完的地方，慢指針就會指向到需要被刪除的節點的前一個節點。

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def removeNthFromEnd(self, head: ListNode, n: int) -> ListNode:
        fast = head
        slow = head
        
        while n > 0:
            fast = fast.next
            n -= 1
        
        if not fast:
            return head.next
        
        while fast and fast.next:
            fast = fast.next
            slow = slow.next
            
        slow.next = slow.next.next
        return head
```

