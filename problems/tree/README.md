# Tree 樹

樹是所有技術面試中的題目，投資報酬率最高的題目，不過一開始面對題目時很容易無從下手，尤其是樹的遍歷就是一個遞迴的形式。

題目可以千變萬化，可是不外乎是以下幾種變形，而且自己寫幾次後就能掌握著模式。

### Breadth-first search 廣度優先搜索

BFS 的優勢在於如果要查找圖或是樹的最短距離，BFS 可以在找到目標後快速地停止探索。DFS 在查找最短距離時，要把所有的可行解都找到，才能比較出最短路徑。

另外 BFS 還有一個優勢，那就是 BFS 是可以做到多點同時出發的，把不同的出發點視作是同一層即可，如 [417. Pacific Atlantic Water Flow](pacific-atlantic-water-flow.md) 。

### Depth-first search 深度優先搜索

DFS 是一個遞迴關係式，DFS 的優勢在於如果只是要找到一個目標，在找到目標後就可以停止搜索時，但是和 BFS 的理論時間複雜度是相同的，因為都有可能在最後才找到目標，樹的三種遍歷都是 DFS 的實作之一。

1. [Preorder 前序遍歷](preorder/)
2. [Inorder 中序遍歷](inorder/)
3. [Postorder 後序遍歷](postorder/)

另外 [Backtrack 回溯法](../backtrack/) 也可以看做是一種 DFS 的變形。



