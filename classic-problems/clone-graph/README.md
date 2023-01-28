# Clone Graph 複製圖形

Clone 系列有複製圖形、樹、Linked List ... 等。遍歷的方法並不重要，重要的是要如何快速的查找我們所需要的節點。

這個系列都是屬於使用 Hash Table 的解法，那 Hash Table 可以做什麼呢？**Hash Table 可以用來做一個原圖型和複製的圖形快速的 1:1 映射（這個概念在** [**138. Copy List with Random Pointer**](copy-list-with-random-pointer.md) **會大大的體現 ）**，這使得我們在遍歷圖形的時候，可以快速的找到我們要將複製的節點，加到哪一個對應的節點上面。
