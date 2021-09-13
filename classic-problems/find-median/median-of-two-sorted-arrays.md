# 4. Median of Two Sorted Arrays

[4. Median of Two Sorted Arrays](https://leetcode.com/problems/median-of-two-sorted-arrays/)

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

