# 973. K Closest Points to Origin

[973. K Closest Points to Origin](https://leetcode.com/problems/k-closest-points-to-origin/)

這一個題目要找的是 k 個最靠近原點的點，所以有兩個步驟要處理。

第一個是要先寫出如何計算出距離的公式。

第二個是可以利用 heap 的特色，保持 k 個最小值的特色，只是這裡要 pop 掉的是最大值，所以存進去時，要用 max heap 的方式來做。

```python
class Solution:
    def kClosest(self, points: List[List[int]], k: int) -> List[List[int]]:
        heap = []
        heapq.heapify(heap)
        
        def getDest(x, y):
            return (x**2 + y**2)**0.5
        
        for x, y in points:
            dest = getDest(x, y)
            if len(heap) == k:
                heapq.heappush(heap, (-dest, [x, y]))
                heapq.heappop(heap)
            else:
                heapq.heappush(heap, (-dest, [x, y]))
            
        return [value for key, value in heap]
```

Python 的 heap API 可以簡化 L12L13

```python
class Solution:
    def kClosest(self, points: List[List[int]], k: int) -> List[List[int]]:
        heap = []
        heapq.heapify(heap)
        
        def getDest(x, y):
            return (x**2 + y**2)**0.5
        
        for x, y in points:
            dest = getDest(x, y)
            if len(heap) == k:
                heapq.heappushpop(heap, (-dest, [x, y]))
            else:
                heapq.heappush(heap, (-dest, [x, y]))
            
        return [value for key, value in heap]
```

