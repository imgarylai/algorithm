# The Maze 球滾迷宮問題

### BFS

```python
class Solution:
    def hasPath(self, maze: List[List[int]], start: List[int], destination: List[int]) -> bool:
        if not maze or not maze[0]: return False
        rows = len(maze)
        columns = len(maze[0])
        directions = [(0, 1), (1, 0), (0, -1), (-1, 0)]
        q = deque([start])
        maze[start[0]][start[1]] = 2
        while q:
            r, c = q.popleft()
            for dr, dc in directions:
                next_r = r
                next_c = c
                while 0 <= next_r + dr < rows and 0 <= next_c + dc < columns and maze[next_r+dr][next_c+dc] != 1:
                    next_r += dr
                    next_c += dc
                if maze[next_r][next_c] == 0:       
                    if next_r == destination[0] and next_c == destination[1]:
                        return True
                    q.append((next_r, next_c))
                    maze[next_r][next_c] = 2
        return False
```

