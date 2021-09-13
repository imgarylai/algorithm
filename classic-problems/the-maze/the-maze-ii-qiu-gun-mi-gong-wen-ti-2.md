# The Maze II 球滾迷宮問題 2

### BFS

```python
class Solution:
    def shortestDistance(self, maze: List[List[int]], start: List[int], destination: List[int]) -> int:
        if not maze or not maze[0]: return False
        
        rows = len(maze)
        columns = len(maze[0])
        distance = [[float('inf')] * columns for _ in range(rows)]
        directions = [(0, 1), (1, 0), (0, -1), (-1, 0)]
        distance[start[0]][start[1]] = 0
        q = deque([start])
        
        while q:
            r, c = q.popleft()
            for dr, dc in directions:
                next_r = r
                next_c = c
                next_dist = 0
                while 0 <= next_r + dr < rows and 0 <= next_c + dc < columns and maze[next_r+dr][next_c+dc] != 1:
                    next_r += dr
                    next_c += dc
                    next_dist += 1
                if distance[r][c] + next_dist < distance[next_r][next_c]:
                    distance[next_r][next_c] = distance[r][c] + next_dist
                    if next_r == destination[0] and next_c == destination[1]:
                        continue
                    q.append((next_r, next_c))

        shortest_distance = distance[destination[0]][destination[1]]
        return -1 if shortest_distance == float('inf') else shortest_distance;
```

