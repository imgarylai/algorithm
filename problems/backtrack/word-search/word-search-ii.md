# 212. Word Search II

[212. Word Search II](https://leetcode.com/problems/word-search-ii/)

這一題是 [79. Word Search](./) 的進階版，原先我們要找的是給定一個字串，看這個一個字串是否存在，這題是給定很多字串，要看哪些字串存在？

第一個直覺的想法是，那就把第一題的解法把字串一個一個檢查就好，但是這樣的方法很明顯會超時。

```python
class Solution:
    def findWords(self, board: List[List[str]], words: List[str]) -> List[str]:
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
                        board[r][c] = word[0]
                        return True
                board[r][c] = word[0]
            return False
        ans = set()

        for word in set(words):
            for r in range(rows):
                for c in range(cols):
                    if backtrack(r, c, word):
                        ans.add(word)
        return ans
```

## Trie

這個解法其實滿特別的，我依稀有想到，但是實作的細節還是有點難，LeetCode 上面是直接寫出了解答，但是我覺得如何去思考出這個想法才是最困難的。

其實上面的暴力解，其實我們已經做了很多剪枝的動作，但是是一個字串一個字串開始搜尋，如果說今天有兩個字串，`abcdef` 和`abcdeg` 在上面的那個做法就會很浪費時間，因為在 `abcdef` 時，我們就已經知道了 `abcde` 的存在，只差一步之遙，就可以找到 `g` 了。**只要附近還有節點沒有搜索過，是不是就應該要再加油一點去看看？**

想到了這裡，其實方向很像是動態規劃，我甚至覺得這也算是動態規劃的一種變形？以這個例子來說，我們要是在搜尋的時候可以一起搜尋類似的字串，那這樣不是很好嗎？這個題目困難在是否可以一直想到這一步，因為要搜尋類似的字串，就可以想到就會需要使用 `Trie` 。

第一個步驟就是，把我們想要搜尋的字串先轉換成 Trie ，**並且要在結尾處標記是哪個單字**，方便之後直接找出結果。

接下來依然是回朔法，但是我們透過 Trie 可以更大量的減少搜索空間

### 第一步

在遍歷矩陣時，要先注意矩陣的元素是否是在 Trie 的根節點？如果沒有的話，代表從那個點出發一定不會有我們目標的字串

### 第二步

先取得該節點，如果該節點有 Trie 的結束標記符號，代表我們找到了目標字串之一，加到答案裡面。

### 第三步

開始向下探索，要確定三件事情

1. 是否在邊界裡面？
2. 有沒有在目前 Trie Node 的子節點裡面？
3. 是否有造訪過？

回溯方法基本就結束了

```python
class Solution:
    def findWords(self, board: List[List[str]], words: List[str]) -> List[str]:
        rows = len(board)
        cols = len(board[0])
        directions = [(1,0),(0,1),(-1,0),(0,-1)]
        trie = {}

        for word in words:
            node = trie
            for char in word:
                node = node.setdefault(char, {})
            node['$'] = word
        ans = set()

        def backtrack(row, col, visited, root):
            node = root[board[row][col]]
            if '$' in node.keys():
                ans.add(node['$'])
            visited.add((row, col))
            for dr, dc in directions:
                nr, nc = row + dr, col + dc
                if 0 <= nr < rows and 0 <= nc < cols and board[nr][nc] in node and (nr, nc) not in visited:
                    backtrack(nr, nc, visited, node)
            visited.remove((row, col))

        for row in range(rows):
            for col in range(cols):
                if board[row][col] in trie:
                    backtrack(row, col, set(), trie)
        return ans
```

