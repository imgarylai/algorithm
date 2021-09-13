# 174. Dungeon Game

[174. Dungeon Game](https://leetcode.com/problems/dungeon-game/)



```python
class Solution:
    def calculateMinimumHP(self, dungeon: List[List[int]]) -> int:
        
        rows = len(dungeon)
        cols = len(dungeon[0])
        memo = {}

        def helper(row, col):
            if row == rows - 1 and col == cols - 1:
                return 1 if dungeon[row][col] >= 0 else -dungeon[row][col] + 1;
            
            if row == rows or col == cols:
                return float('inf')
            
            if (row, col) in memo:
                return memo[(row, col)]
            
            res = min(helper(row + 1, col), helper(row, col + 1)) - dungeon[row][col]
            memo[(row, col)] = 1 if res <= 0 else res
            return memo[(row, col)]

        return helper(0, 0)
```

