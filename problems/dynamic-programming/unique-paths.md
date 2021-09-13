# 62. Unique Paths

[62. Unique Paths](https://leetcode.com/problems/unique-paths/)

### 自頂向下

```python
class Solution:
    def uniquePaths(self, m: int, n: int) -> int:
        memo = {}
        def dp(row, col):
            if row == 1 or col == 1:
                return 1
            if (row, col) in memo:
                return memo[(row, col)]
            memo[(row, col)] = dp(row-1, col) + dp(row, col-1)
            return memo[(row, col)]
        return dp(m, n)
```

### 自底向上

```python
class Solution:
    def uniquePaths(self, m: int, n: int) -> int:
        # 建立出動態規劃自底向上的表格
        dp = [[0 for _ in range(n)] for _ in range(m)]
        
        # Base Case 1
        # 從起點一直向右走到底都是只有一種路徑
        for row in range(m):
            dp[row][0] = 1

        # Base Case 2
        # 從起點一直向下走都是只有一種路徑
        for col in range(n):
            dp[0][col] = 1
        
        for i in range(1, m):
            for j in range(1, n):
                dp[i][j] = dp[i - 1][j] + dp[i][j - 1]
        
        return dp[m-1][n-1]
```

上面 Base Case 的情況可以合併一起處理：

```python
class Solution:
    def uniquePaths(self, m: int, n: int) -> int:
        dp = [[1 for _ in range(n)] for _ in range(m)]
        
        for i in range(1, m):
            for j in range(1, n):
                dp[i][j] = dp[i - 1][j] + dp[i][j - 1]
        
        return dp[m-1][n-1]
```

