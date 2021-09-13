# 429. N-ary Tree Level Order Traversal

[429. N-ary Tree Level Order Traversal](https://leetcode.com/problems/n-ary-tree-level-order-traversal/)

```python
"""
# Definition for a Node.
class Node:
    def __init__(self, val=None, children=None):
        self.val = val
        self.children = children
"""

class Solution:
    def levelOrder(self, root: 'Node') -> List[List[int]]:
        if not root:
            return root
        queue = deque([root])
        ans = defaultdict(list)
        level = 0
        while queue:
            size = len(queue)
            for i in range(size):
                node = queue.popleft()
                ans[level].append(node.val)
                for child in node.children:
                    queue.append(child)
            level += 1
        return ans.values()
```

