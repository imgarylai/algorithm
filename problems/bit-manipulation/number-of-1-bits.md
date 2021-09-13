# 191. Number of 1 Bits

[191. Number of 1 Bits](https://leetcode.com/problems/number-of-1-bits/)

確定最後一位是不是 1 ，是的話就增加計數器，檢查完後就整個往右移一位。

```python
class Solution:
    def hammingWeight(self, n: int) -> int:
        ans = 0

        while n:
            ans += n & 1
            n = n >> 1

        return ans
```

特殊技巧

```python
class Solution:
    def hammingWeight(self, n: int) -> int:
        ans = 0

        while n:
            n = n & (n - 1)
            ans += 1

        return ans
```

