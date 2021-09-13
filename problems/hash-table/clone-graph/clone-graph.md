# 133. Clone Graph

[133. Clone Graph](https://leetcode.com/problems/clone-graph/)

這一題雖然會用到 Graph 的遍歷，BFS 或是 DFS 都可以，不過真正需要理解的核心並不是遍歷，因為這個題目的遍歷並不難。

因為這個題目是一個圖，所以說要確定可以遍歷完所以的節點，又確保不會走過已經走過的路，最重要的就是要記憶過自己走過哪裡。

### 廣度優先搜索

```python
"""
# Definition for a Node.
class Node:
    def __init__(self, val = 0, neighbors = None):
        self.val = val
        self.neighbors = neighbors if neighbors is not None else []
"""

class Solution:
    def cloneGraph(self, node: 'Node') -> 'Node':
        if not node:
            return node
    
        queue = deque([node])
        visited = {}
        visited[node] = Node(node.val)

        while queue:
            root = queue.popleft()
            for neighbor in root.neighbors:
                if neighbor not in visited:
                    visited[neighbor] = Node(neighbor.val, [])
                    queue.append(neighbor)
                visited[root].neighbors.append(visited[neighbor])

        return visited[node]
```

### 深度優先搜索

```python
"""
# Definition for a Node.
class Node:
    def __init__(self, val = 0, neighbors = None):
        self.val = val
        self.neighbors = neighbors if neighbors is not None else []
"""

class Solution:
    def cloneGraph(self, node: 'Node') -> 'Node':
        visited = {}

        def dfs(node):
            if not node:
                return node
            if node in visited:
                return visited[node]

            clone = Node(node.val, [])
            visited[node] = clone

            if node.neighbors:
                clone.neighbors = [dfs(n) for n in node.neighbors]
            return clone

        return dfs(node)
```

