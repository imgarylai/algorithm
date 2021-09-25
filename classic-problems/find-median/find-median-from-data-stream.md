# 295. Find Median from Data Stream

[295. Find Median from Data Stream](https://leetcode.com/problems/find-median-from-data-stream/)

這題如果透過排序的話，就會很好做，但是如果只是排序的話，時間複雜度是 $$O(nlogn)$$ 

這題要利用的是 `Heap` 的特性，只要我們可以讓「最大」或是「最小」的數字始終保持在樹的最上方。

這樣的話時間複雜度可以保持在 $$O(logn)$$ 

```python
import heapq
class MedianFinder:

    def __init__(self):
        """
        initialize your data structure here.
        """
        self.max_heap = []
        self.min_heap = []
        heapq.heapify(self.max_heap)
        heapq.heapify(self.min_heap)

    def addNum(self, num: int) -> None:
        if not self.max_heap or num < -self.max_heap[0]:
            heapq.heappush(self.max_heap, -num)
        else:
            heapq.heappush(self.min_heap, num)

        if len(self.max_heap) > len(self.min_heap):
            heapq.heappush(self.min_heap, -heapq.heappop(self.max_heap))
        if len(self.max_heap) < len(self.min_heap):
            heapq.heappush(self.max_heap, -heapq.heappop(self.min_heap))

    def findMedian(self) -> float:
        if len(self.max_heap) > len(self.min_heap):
            return float(-self.max_heap[0])
        elif len(self.max_heap) < len(self.min_heap):
            return float(self.min_heap[0])
        else:
            return float(self.min_heap[0] + -self.max_heap[0]) / 2


# Your MedianFinder object will be instantiated and called as such:
# obj = MedianFinder()
# obj.addNum(num)
# param_2 = obj.findMedian()
```

