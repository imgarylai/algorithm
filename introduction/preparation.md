# 事前準備

## 資料

### 儲存結構

儲存的結構有很多種，但是最底層以 Array 和 Linked List 為主。

### 操作

不外乎就是**增、刪、查、改**，英文世界裡常見的 CRUD \(Create, Read, Update, Delete\) 。電腦執行就是要盡可能的高效率的去完成以上幾個動作，因此就衍伸出了**時間複雜度**，而當資料用不同的方式儲存時就會有不同的**空間複雜度**，因此不同的演算法的目的就是要想辦法優化兩者的複雜度，或是在中間取得一個最佳的平衡。

不同的儲存結構與操作有時候可以完成一樣的事情

* 資料用陣列儲存，用 `for` 迴圈印出每一格的資料

```python
for i in range(len(arr)):
    print(arr[i])
```

* 資料用陣列儲存，用 `while` 迴圈印出每一格的資料

```python
while i < len(arr):
    print(arr[i])
    i += 1
```

* 資料用陣列儲存，用遞迴的方式印出每一格的資料

```python
# arr = [...]
def recursive(i):
    if i < len(arr):
        print(arr[i])
        recursive(i+1)
```

* 資料用 Linked List 儲存，用 `while` 迴圈印出每一格的資料

```python
# Definition for a node.
# class Node:
#     def __init__(self, val: int = 0, next: Node = None):
#         self.val = val
#         self.next = next

while node:
    print(node.val)
    node = node.next
```

* 有些程式語言例如：Java ，資料用 Linked List 儲存，可以用 for 迴圈印出每一格的資料

```java
/*    
class Node {
        int val;
        Node next;
}
*/
for (Node p = head; p != null; p = p.next) {
    System.out.println(p.val)
}
```

* 資料用 Linked List 儲存，可以用遞迴的方式印出每一格的資料

```python
def traverse(node: Node):
    if not node:
        return
    print(node.val)
    traverse(node.next)
```

