# 286. Walls and Gates

[286. Walls and Gates](https://leetcode.com/problems/walls-and-gates/)

這題是 BFS 廣度優先搜索的題目，DFS 應該也可以做。

我一開始的做法是把 BFS 的邏輯抽出來寫如下，但是這樣做會超時，因為其實這樣做除了 BFS 的時間複雜度以外，其實重複的路徑會一直走。

```python
class Solution:
    def wallsAndGates(self, rooms: List[List[int]]) -> None:
        """
        Do not return anything, modify rooms in-place instead.
        """  
        directions = [(1, 0), (-1, 0), (0, 1), (0, -1)]
        def bfs(row, col):
            queue = deque()
            queue.append((row, col))
            while queue:
                row, col = queue.popleft()
                for dr, dc in directions:
                    nr = row + dr
                    nc = col + dc
                    if 0 <= nr < rows and 0 <= nc < cols and rooms[nr][nc] > rooms[row][col]:
                        rooms[nr][nc] = rooms[row][col] + 1
                        queue.append((nr, nc))

        rows = len(rooms)
        cols = len(rooms[0])
        
        for row in range(rows):
            for col in range(cols):
                if rooms[row][col] == 0:
                    bfs(row, col)
```

不過其實這題稍微特別一點，可以把所有的出發地點都先放進去 `queue` ，同時一起探索，這樣的話速度會快很多。 

```python
class Solution:
    def wallsAndGates(self, rooms: List[List[int]]) -> None:
        """
        Do not return anything, modify rooms in-place instead.
        """  

        rows = len(rooms)
        cols = len(rooms[0])
        queue = deque()
        for row in range(rows):
            for col in range(cols):
                if rooms[row][col] == 0:
                    queue.append((row, col))
                    
        directions = [(1, 0), (-1, 0), (0, 1), (0, -1)]
        
        while queue:
            row, col = queue.popleft()
            for dr, dc in directions:
                nr = row + dr
                nc = col + dc
                if 0 <= nr < rows and 0 <= nc < cols and rooms[nr][nc] > rooms[row][col]:
                    rooms[nr][nc] = rooms[row][col] + 1
                    queue.append((nr, nc))
```

