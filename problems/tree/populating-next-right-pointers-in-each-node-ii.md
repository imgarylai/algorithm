# 117. Populating Next Right Pointers in Each Node II

[117. Populating Next Right Pointers in Each Node II](https://leetcode.com/problems/populating-next-right-pointers-in-each-node-ii/)

```python
"""
# Definition for a Node.
class Node:
    def __init__(self, val: int = 0, left: 'Node' = None, right: 'Node' = None, next: 'Node' = None):
        self.val = val
        self.left = left
        self.right = right
        self.next = next
"""

class Solution:
    def connect(self, root: 'Node') -> 'Node':
        if not root:
            return root
        q = [root]
        
        while q:
            size = len(q)
            for i in range(size):
                node = q.pop(0)
                if i < size - 1:
                    node.next = q[0]
                if node.left:
                    q.append(node.left)
                if node.right: 
                    q.append(node.right)
                    
        return root
        
```



