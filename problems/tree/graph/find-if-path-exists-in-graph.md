# 1971. Find if Path Exists in Graph

[1971. Find if Path Exists in Graph](https://leetcode.com/problems/find-if-path-exists-in-graph/)



```python
class Solution:
    def validPath(self, n: int, edges: List[List[int]], start: int, end: int) -> bool:
        if not edges:
            return start == end
        
        table = defaultdict(list)
        for edge in edges:
            table[edge[0]].append(edge[1]) 
            table[edge[1]].append(edge[0])
            
        queue = deque([start])
        
        visited = set() 
        while queue:
            node = queue.popleft()
            visited.add(node)
            for child in table[node]:
                if child == end:
                    return True
                if child not in visited:
                    queue.append(child)
        
        return False
```

