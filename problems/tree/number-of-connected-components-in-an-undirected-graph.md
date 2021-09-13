# 323. Number of Connected Components in an Undirected Graph

可以繼承 547 的做法，先轉換給定的 edges 成一個矩陣。

{% page-ref page="number-of-provinces.md" %}

```python
class Solution:
    def countComponents(self, n: int, edges: List[List[int]]) -> int:
        matrix = [[0]*n for _ in range(n)]
        for edge in edges:
            matrix[edge[0]][edge[1]] = 1
            matrix[edge[1]][edge[0]] = 1
        
        visited = set()
        count = 0
        
        def dfs(i):
            for j in range(n):
                if matrix[i][j] == 1 and j not in visited:
                    visited.add(j)
                    dfs(j)
        
        for i in range(n):
            if i not in visited:
                visited.add(i)
                dfs(i)
                count += 1
        return count
```

但是這樣的速度太慢了，時間複雜度是 O\(n^2\) ，空間複雜度也是 O\(n^2\)。我們可以更一步的精簡，那就是把需要搜索的路徑記錄起來就好了。

記錄的方式可以透過 Hash Table ，key 是島嶼的編號，value 是一個陣列，包含了所有的 edges 。

```python
class Solution:
    def countComponents(self, n: int, edges: List[List[int]]) -> int:
        graph = {}
        visited = set()
        count = 0
        for i in range(n):
            graph[i] = []
        for edge in edges:
            graph[edge[0]].append(edge[1])
            graph[edge[1]].append(edge[0])    
        def dfs(i):
            for j in graph[i]:
                if j not in visited:
                    visited.add(j)
                    dfs(j)
        for i in range(n):
            if i not in visited:
                visited.add(i)
                dfs(i)
                count += 1
        return count
```

Hash Table 的方式也可以用陣列的取代

```python
graph = [[] for _ in range(n)]
for edge in edges:
    graph[edge[0]].append(edge[1])
    graph[edge[1]].append(edge[0])    
```

