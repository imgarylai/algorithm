# 1490. Clone N-ary Tree

[1490. Clone N-ary Tree](https://leetcode.com/problems/clone-n-ary-tree/)

和 [133. Clone Graph](clone-graph.md) 的意義相同

## DFS

```python
"""
# Definition for a Node.
class Node:
    def __init__(self, val=None, children=None):
        self.val = val
        self.children = children if children is not None else []
"""

class Solution:
    def cloneTree(self, root: 'Node') -> 'Node':
        table = {}
        def dfs(node):
            if not node:
                return None
            table[node] = Node(node.val, [])
            table[node].children = [dfs(child) for child in node.children]
            return table[node]
        return dfs(root)
```

## BFS

```python
"""
# Definition for a Node.
class Node:
    def __init__(self, val=None, children=None):
        self.val = val
        self.children = children if children is not None else []
"""

class Solution:
    def cloneTree(self, root: 'Node') -> 'Node':
        if not root:
            return root
        table = {}
        queue = deque([root])
        table[root] = Node(root.val)
        while queue:
            node = queue.popleft()
            for child in node.children:
                queue.append(child)
                table[child] = Node(child.val)
                table[node].children.append(table[child])
        return table[root]
```
