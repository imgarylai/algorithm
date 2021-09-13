# 7. Reverse Integer

[7. Reverse Integer](https://leetcode.com/problems/reverse-integer/)

```python
class Solution:
    def reverse(self, x: int) -> int:  
        res = 0
        sign = x > 0
        x = abs(x)
        while x > 0:
            res = res * 10 + x % 10
            x //= 10
        res = res if sign else -res
        return res if res.bit_length() < 32 else 0
```

