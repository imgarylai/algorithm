# 329. Longest Increasing Path in a Matrix

[329. Longest Increasing Path in a Matrix](https://leetcode.com/problems/longest-increasing-path-in-a-matrix/)

DFS + Memorization 

```python
class Solution:
    def longestIncreasingPath(self, matrix: List[List[int]]) -> int:
        rows = len(matrix)
        cols = len(matrix[0])
        directions = [(1,0),(0,1),(-1,0),(0,-1)]
        ans = defaultdict(int)
        def findMaxLength(row: int, col: int) -> int:
            if (row,col) in ans:
                return ans[(row,col)]
            for dr, dc in directions:
                nr, nc = row + dr, col + dc
                if 0 <= nr < rows and 0 <= nc < cols and matrix[nr][nc] > matrix[row][col]:
                    ans[(row,col)] = max(ans[(row,col)], findMaxLength(nr, nc))
            ans[(row,col)] += 1
            return ans[(row,col)]
        for row in range(rows):
            for col in range(cols):
                findMaxLength(row, col)
        return max(ans.values())
```

