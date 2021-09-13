# 100. Same Tree

[100. Same Tree](https://leetcode.com/problems/same-tree/)

### DFS

每次都往同樣的方向走，去比較是否一樣

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def isSameTree(self, p: TreeNode, q: TreeNode) -> bool:
        if not p and not q:
            return True
        if not p or not q or p.val != q.val:
            return False
        return self.isSameTree(p.left, q.left)  and self.isSameTree(p.right, q.right)
```

### BFS

一起放進 queue 裡面做 BFS 

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def isSameTree(self, p: TreeNode, q: TreeNode) -> bool:
        queue = deque([(p, q)])
        
        while queue:
            a, b = queue.popleft()
            if a and b and a.val == b.val:
                queue.extend([(a.left, b.left), (a.right, b.right)])
            elif a or b:
                return False
        
        return True
```

