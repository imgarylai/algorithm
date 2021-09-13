# 79. Word Search

[79. Word Search](https://leetcode.com/problems/word-search/)

這一題用的是回溯算法，接著從矩陣的每個字元開始出發，首先會先判斷兩件事情：

1. 是否超過邊界？
2. 該座標的是不是目標字串的第一個字？

如果是的話才會開始向下搜尋，向下搜尋的時候要注意兩件事情

1. 要記得將目前的座標標記成為已造訪
2. 向下傳遞時，是傳遞目標字串的 `word[1:]` 

終止條件是字串搜尋完畢

```python
class Solution:
    def exist(self, board: List[List[str]], word: str) -> bool:
        rows = len(board)
        cols = len(board[0])
        directions = [(1,0),(-1,0),(0,1),(0,-1)]
        def backtrack(r, c, word):
            if len(word) == 0:
                return True
            if 0 <= r < rows and 0 <= c < cols and board[r][c] == word[0]:
                board[r][c] = '#'
                for dr, dc in directions:
                    if backtrack(r+dr, c+dc, word[1:]):
                        return True
                board[r][c] = word[0]
            return False
            
        for r in range(rows):
            for c in range(cols):
                if backtrack(r, c, word):
                    return True
        return False
```

