# 115. Distinct Subsequences

[115. Distinct Subsequences](https://leetcode.com/problems/distinct-subsequences/)

```python
class Solution:
    def numDistinct(self, s: str, t: str) -> int:

        memo = defaultdict(int)
        def helper(i, j):
            if i == len(s) and j == len(t):
               return 1
            elif i == len(s):
                return 0
            elif j == len(t):
                return 1

            if (i, j) in memo:
                return memo[(i, j)]

            if s[i] == t[j]:
                ans = helper(i + 1, j + 1) + helper(i + 1, j)
            else:
                ans = helper(i + 1, j)

            memo[(i, j)] = ans
            return memo[(i, j)]

        return helper(0, 0)
```

