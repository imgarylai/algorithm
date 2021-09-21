# 200. Number of Islands

[200. Number of Islands](https://leetcode.com/problems/number-of-islands/)

1. 要如何標記已經造訪過的元素
2. 如何在矩陣中行走

## DFS

```python
class Solution:
    def numIslands(self, grid: List[List[str]]) -> int:
        if not grid or not grid[0]:
            return 0
        directions = [(1, 0), (0, 1), (-1, 0), (0, -1)]
        rows = len(grid)
        columns = len(grid[0])
        island = 0
        def dfs(r, c):
            grid[r][c] = '#'
            for dr, dc in directions:
                if 0 <= r + dr < rows and 0 <= c + dc < columns and grid[r+dr][c+dc] == '1':
                    dfs(r + dr, c + dc)    
        for i in range(rows):
            for j in range(columns):
                if grid[i][j] == '1':
                    island += 1
                    dfs(grid, i, j)
        return island
```

## BFS

```python
class Solution:
    def numIslands(self, grid: List[List[str]]) -> int:
        if not grid or not grid[0]:
            return 0

        m = len(grid)
        n = len(grid[0])

        islands = 0

        for i in range(m):
            for j in range(n):
                if grid[i][j] == "1":
                    islands += 1
                    q = [(i, j)]
                    while q:
                        x, y = q.pop(0)
                        grid[x][y] = '#'
                        for dx, dy in [(1, 0), (-1, 0), (0, 1), (0, -1)]:
                            new_x, new_y = x + dx, y + dy
                            if 0 <= new_x < m and 0 <= new_y < n and grid[new_x][new_y] == "1":
                                q.append((new_x, new_y))
                                grid[new_x][new_y] = '#'
        return islands
```

