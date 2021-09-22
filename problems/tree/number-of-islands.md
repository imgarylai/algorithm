# 200. Number of Islands

[200. Number of Islands](https://leetcode.com/problems/number-of-islands/)

這一題的重點在於於圖形中，進行深度優先搜索或是廣度優先搜索的遍歷。

今天的題目條件在於，如果一個陸地屬於一個島嶼的話，那該陸地一定是與其他陸地的四個方向之一有相連，要計算出有幾個島嶼，我只要站在島嶼上的任何一塊陸地，把該島嶼全部都標記成已經造訪過，那我就可以確定這個島嶼已經造訪完畢，計數器加一，接著再繼續找到下一個尚未被標記的陸地即可。

### 深度優先搜索

```python
class Solution:
    def numIslands(self, grid: List[List[str]]) -> int:
        rows = len(grid)
        cols = len(grid[0])
        directions = [(1, 0), (0, 1), (-1, 0), (0, -1)]
        
        def dfs(row, col):
            grid[row][col] = '#'
            for dr, dc in directions:
                next_row = row+dr
                next_col = col+dc
                if 0 <= next_row < rows and 0 <= next_col < cols and grid[next_row][next_col] == '1':
                    dfs(next_row, next_col)
                    
        islands = 0
        
        for row in range(rows):
            for col in range(cols):
                if grid[row][col] == '1':
                    islands += 1
                    dfs(row, col)
                    
        return islands 
```

### 廣度優先搜索

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

