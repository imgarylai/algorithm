# 70. Climbing Stairs

[70. Climbing Stairs](https://leetcode.com/problems/climbing-stairs/)

等同於 [509. Fibonacci Number](fibonacci-number.md)  

```python
class Solution:
    def fib(self, n: int):
        p1, p2 = 0, 1
        for i in range(2, n + 1):
            p1, p2 = p2, p1 + p2
        return p2
    
    def climbStairs(self, n: int) -> int:
        return self.fib(n + 1)
```



