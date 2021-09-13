# 875. Koko Eating Bananas

[875. Koko Eating Bananas](https://leetcode.com/problems/koko-eating-bananas/)

```python
class Solution:    
    def minEatingSpeed(self, piles: List[int], h: int) -> int:        
        left = 1
        right = max(piles)
        
        def helper(k: int) -> int:
            hours = 0
            for pile in piles:
                hours += pile // k
                if pile % k > 0:
                    hours += 1
            return hours
        
        while left < right:
            k = left + (right - left) // 2
            if helper(k) <= h:
                right = k
            else:
                left = k + 1
        
        return left
```

