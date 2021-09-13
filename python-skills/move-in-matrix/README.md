# 矩陣的走法

動態規劃的題目有分「自頂向下」以及「自底向上」的解法，很多題目兩種方向都可以實作。

自頂向下的記憶方法是透過遞迴的方式，先找到最小的子問題，並且記憶著答案，再慢慢的回推回需要的答案，其中的記憶方法通常靠 `Hash Table` 就可以完成，只要我們可以知道怎麼組合出適當的 `key` 做為查找子問題答案的關鍵。

自底向上的題目，則是需要先建立好需要的記憶體空間，並且把 Base Case 的答案先建立好，再逐步地把最後的答案寫出來，最經典的就是 [62. Unique Paths](../../problems/dynamic-programming/unique-paths.md#zi-di-xiang-shang) 的題目。 而自底向上比起自頂向下的解法，在某些情況下，我們可以透過壓縮記憶體的位置，進一步的讓程式執行起來更有效率。

自底向上的題目當然有很多種建立記憶體空間的位置，其中最常見的就是透過二維的矩陣去找出排列組合，三維以上的也有，但是相對稀少，通常這個矩陣的遍歷方向也是從左到右，從上到下的遍歷，像是以下是一種常見的情況，這種情況其實相對簡單。

```python
rows = len(matrix)
cols = len(matrix[0])

dp = [[0 for _ in range(cols)] for _ in range(rows)]

for row in range(1, rows):
    for col in range(1, cols):
        dp[row][col] = max(dp[row-1][col-1], dp[row-1][col], dp[row][col-1])
```

困難的是，有些動態規劃的遍歷順序並不是直覺的由左至右、從上到下，例如： [516. Longest Palindromic Subsequence](../../classic-problems/palindrome/longest-palindromic-subsequence.md) 的自底向上的辦法，他需要遍歷的順序是由左上到右下，走上半部的走法。

```text
1  6  10 13 15 
0  2  7  11 14 
0  0  3  8  12 
0  0  0  4  9  
0  0  0  0  5
```

矩陣的走法也可以被當作是一種題目來呈現，像是 [498. Diagonal Traverse](../../problems/array/diagonal-traverse.md) 。 這裡我會整理出所有我想得到的矩陣走法。有時候快速想到這個矩陣走法，可以讓自己在面試的時候更不會慌張，並且有效的解決問題。

接下來的筆記都會用這個方式來印出陣列的移動順序

```python
def print_matrix(matrix):
    for row in range(n):
        for col in range(n):
            print(str(matrix[row][col]).ljust(2), end=' ')
        print()
```

