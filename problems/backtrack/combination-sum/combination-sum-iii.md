# 216. Combination Sum III

[216. Combination Sum III](https://leetcode.com/problems/combination-sum-iii/)

這一題和 [77. Combinations](../combinations.md) 與 [39. Combination Sum](./) 差不多，其實比 [40. Combination II](combination-sum-ii.md) 簡單。

```python
class Solution:
    def combinationSum3(self, k: int, n: int) -> List[List[int]]:
        ans = []
        def backtrack(curr, target, start):
            if target == 0:
                if len(curr) == k:
                    ans.append(list(curr))
                return
            if target < 0:
                return
            else:
                for i in range(start, 10):
                    curr.append(i)
                    backtrack(curr, target - i, i + 1)
                    curr.pop()
        backtrack([], n, 1)
        return ans
```

