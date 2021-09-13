# 1011. Capacity To Ship Packages Within D Days

[1011. Capacity To Ship Packages Within D Days](https://leetcode.com/problems/capacity-to-ship-packages-within-d-days/)

```python
class Solution:
    def shipWithinDays(self, weights: List[int], days: int) -> int:
        left = max(weights)
        right = sum(weights) + 1
        
        def helper(capacity):
            days = 1
            acc = 0
            for weight in weights:
                if acc + weight > capacity:
                    acc = weight
                    days += 1
                else:
                    acc += weight
            return days
        
        while left < right:
            mid = left + (right - left) // 2
            if helper(mid) <= days:
                right = mid
            else:
                left = mid + 1
        
        return left
```

