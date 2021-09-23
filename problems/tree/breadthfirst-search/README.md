# Breadth-first search 廣度優先搜索

BFS 的優勢在於如果要查找圖或是樹的最短距離，BFS 可以在找到目標後快速地停止探索。DFS 在查找最短距離時，要把所有的可行解都找到，才能比較出最短路徑。

有些題目並沒有很明確的是圖或是樹的題目，但是其實也是要尋找最短路徑，這種題目的困難在於我們要如後透過當下的狀態，判斷出子樹長什麼樣子。

* [752. Open the Lock](open-the-lock.md)
* [Word Ladder 文字梯問題](../../../classic-problems/word-ladder/)

另外 BFS 還有一個優勢，那就是 BFS 是可以做到多點同時出發的，把不同的出發點視作是同一層即可，有些題目甚至一定要這樣做，因為這樣可以節省很多時間。

* [286. Walls and Gates](walls-and-gates.md)
* [417. Pacific Atlantic Water Flow](pacific-atlantic-water-flow.md) 
* [994. Rotting Oranges](rotting-oranges.md)

