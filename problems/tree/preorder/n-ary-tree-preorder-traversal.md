# 589. N-ary Tree Preorder Traversal

[589. N-ary Tree Preorder Traversal](https://leetcode.com/problems/n-ary-tree-preorder-traversal/)

```python
"""
# Definition for a Node.
class Node:
    def __init__(self, val=None, children=None):
        self.val = val
        self.children = children
"""

class Solution:
    def preorder(self, root: 'Node') -> List[int]:
        if not root:
            return []
        res = []
        res.append(root.val)
        for child in root.children:
            res.extend(self.preorder(child))
        return res
```

