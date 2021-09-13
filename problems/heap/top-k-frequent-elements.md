# 347. Top K Frequent Elements

[347. Top K Frequent Elements](https://leetcode.com/problems/top-k-frequent-elements/)

```python
class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:

        counter = Counter(nums)

        pq = []

        heapq.heapify(pq)

        for key in counter.keys():
            heapq.heappush(pq, (-counter[key], key))

        res = []

        while k > 0:
            value, key = heapq.heappop(pq)
            res.append(key)
            k -= 1

        return res
```

