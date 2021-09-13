# 261. Graph Valid Tree

dfs 搜尋的重點是，鄰居可以是 parent ，但是如果不是 parent 卻曾經造訪過，就代表這棵樹裡面有閉圈。

```python
class Solution:
    def validTree(self, n: int, edges: List[List[int]]) -> bool:
        if len(edges) != n - 1: return False

        graph = [[] for _ in range(n)]
        for edge in edges:
            graph[edge[0]].append(edge[1])
            graph[edge[1]].append(edge[0])

        seen = set()

        def dfs(node, parent):
            if node in seen: return
            seen.add(node)
            for nei in graph[node]:
                if nei == parent:
                    continue
                if nei in seen:
                    return False
                res = dfs(nei, node)
                if not res: return False
            return True    
        return dfs(0, -1) and len(seen) == n
```

