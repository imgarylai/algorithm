# 69. Sqrt\(x\)

[69. Sqrt\(x\)](https://leetcode.com/problems/sqrtx/)

```python
class Solution:
    def mySqrt(self, x: int) -> int:        
        if x == 1:
            return 1
        left = 1
        right = x // 2
        while left <= right:
            mid = left + (right - left) // 2
            num = mid * mid
            if num == x:
                return mid
            elif num < x:
                left = mid + 1
            elif num > x:
                right = mid - 1
        return right
```

