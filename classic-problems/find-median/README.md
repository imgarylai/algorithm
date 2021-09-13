# Find Median 尋找中位數

這題如果透過排序的話，就會很好做，但是如果只是排序的話，時間複雜度是 O\(N Log N\)

這題要利用的是 Heap 的特性，只要我們可以讓「最大」或是「最小」的數字始終保持在樹的最上方。

```python
class Solution:
    def findMedianSortedArrays(self, nums1: List[int], nums2: List[int]) -> float:
        min_heap = []
        max_heap = []
        
        def balance_heap(num):
            if len(min_heap) >= len(max_heap):
                top = heapq.heappushpop(min_heap, num)
                heapq.heappush(max_heap, -top)
                
            elif len(min_heap) < len(max_heap):
                top = heapq.heappushpop(max_heap, -num)
                heapq.heappush(min_heap, -top)     

        for num in nums1:
            balance_heap(num)
            
        for num in nums2:
            balance_heap(num)
        
        if len(min_heap) > len(max_heap):
            return heapq.heappop(min_heap)
        elif len(min_heap) < len(max_heap):
            return -heapq.heappop(max_heap)
        else:
            return (heapq.heappop(min_heap) - heapq.heappop(max_heap)) / 2
```

