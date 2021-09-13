# 64. Minimum Path Sum

[64. Minimum Path Sum](https://leetcode.com/problems/minimum-path-sum/)

從最後一個位置向原點出發，每次都往總和比較小的路徑前進，直到原點為止，找出最小的總和

## 遞迴

```python
class Solution:
    def minPathSum(self, grid: List[List[int]]) -> int:
        rows = len(grid)
        cols = len(grid[0])

        def helper(row, col):
            if row < 0 or col < 0:
                return float('inf')
            if row == 0 and col == 0:
                return grid[row][col]
            return min(
                dp(row-1, col), 
                dp(row, col-1)
            ) + grid[row][col]

        return helper(rows-1, cols-1)
```

## 自頂向下

```python
class Solution:
    def minPathSum(self, grid: List[List[int]]) -> int:
        rows = len(grid)
        cols = len(grid[0])
        memo = [[-1] * cols for _ in range(rows)]
        memo[0][0] = grid[0][0]

        def dp(row, col):
            if row < 0 or col < 0:
                return float('inf')
            if memo[row][col] != -1:
                return memo[row][col]
            memo[row][col] = min(
                dp(row-1, col), 
                dp(row, col-1)
            ) + grid[row][col]
            return memo[row][col]
        return dp(rows-1, cols-1)
```

```python
class Solution:
    def minPathSum(self, grid: List[List[int]]) -> int:
        rows = len(grid)
        cols = len(grid[0])

        memo = {}
        memo[(0, 0)] = grid[0][0]
        def dp(row, col):
            if row < 0 or col < 0:
                return float('inf')
            if (row, col) not in memo:
                memo[(row, col)] = min(dp(row-1, col), dp(row, col-1)) + grid[row][col]

            return memo[(row, col)]

        return dp(rows-1, cols-1)
```

## 自底向上

```python
class Solution:
    def minPathSum(self, grid: List[List[int]]) -> int:
        rows = len(grid)
        cols = len(grid[0])

        memo = [[-1] * cols for _ in range(rows)]
        memo[rows-1][cols-1] = grid[rows-1][cols-1]

        for row in reversed(range(rows-1)):
            memo[row][cols-1] = memo[row+1][cols-1] + grid[row][cols-1]
        for col in reversed(range(cols-1)):
            memo[rows-1][col] = memo[rows-1][col+1] + grid[rows-1][col]
        print(memo)
        for row in reversed(range(rows-1)):
            for col in reversed(range(cols-1)):
                memo[row][col] = min(memo[row+1][col], memo[row][col+1]) + grid[row][col]

        return memo[0][0]
```

從原點向終點出發

## 遞迴

```python
class Solution:
    def minPathSum(self, grid: List[List[int]]) -> int:
        rows = len(grid)
        cols = len(grid[0])

        def dp(row, col):
            if row == rows - 1 and col == cols - 1:
                return grid[row][col]
            if row >= rows or col >= cols:
                return float('inf')
            return grid[row][col] + min(dp(row+1, col), dp(row, col+1))
        return dp(0, 0)
```

## 自頂向下

```python
class Solution:
    def minPathSum(self, grid: List[List[int]]) -> int:
        rows = len(grid)
        cols = len(grid[0])

        memo = {}
        memo[(rows-1,cols-1)] = grid[rows-1][cols-1]
        def dp(row, col):
            if row >= rows or col >= cols:
                return float('inf')
            if (row, col) not in memo:
                memo[(row, col)] = grid[row][col] + min(dp(row+1, col), dp(row, col+1))
            return memo[(row, col)]
        return dp(0, 0)
```

## 自底向上

```python
class Solution:
    def minPathSum(self, grid: List[List[int]]) -> int:
        rows = len(grid)
        cols = len(grid[0])
        memo = [[-1] * cols for _ in range(rows)]
        memo[0][0] = grid[0][0]
        for row in range(1, rows):
            memo[row][0] = memo[row-1][0] + grid[row][0]
        for col in range(1, cols):
            memo[0][col] = memo[0][col-1] + grid[0][col]

        for row in range(1, rows):
            for col in range(1, cols):
                memo[row][col] = min(memo[row-1][col], memo[row][col-1]) + grid[row][col]

        return memo[rows-1][cols-1]
```

