# 973. K Closest Points to Origin

[973. K Closest Points to Origin](https://leetcode.com/problems/k-closest-points-to-origin/)

```python
class Solution:
    def kClosest(self, points: List[List[int]], k: int) -> List[List[int]]:
        q = []
        heapq.heapify(q)
        def dest(x, y):
            return x**2 + y**2
        for x, y in points:
            if len(q) == k:
                heapq.heappushpop(q, (-dest(x, y), [x, y]))
            else:
                heapq.heappush(q, (-dest(x, y), [x, y]))

        return [value for key, value in q]
```

