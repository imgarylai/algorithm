# 1446. Consecutive Characters

[1446. Consecutive Characters](https://leetcode.com/problems/consecutive-characters/)

```python
class Solution:
    def maxPower(self, s: str) -> int:
        prev = s[0]
        count = 1
        res = 1
        for curr in range(1, len(s)):
            if s[curr] == prev:
                count += 1
                res = max(res, count)
            else:
                prev = s[curr]
                count = 1
        return res
```

