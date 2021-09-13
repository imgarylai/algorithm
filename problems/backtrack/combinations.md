# 77. Combinations

[77. Combinations](https://leetcode.com/problems/combinations/)

這一個題目的精神和我們平常窮舉的精神一樣，我們先從最小的數字開始，慢慢地的和比自己大的樹去取組合，列完後，找到次小的數字，重複同樣的動作。

我們從 `1` 開始，一直到 `n + 1` ，看看有幾種組合，每往下探索的時候，我們要從下一個數字來開始看。

```python
class Solution:
    def combine(self, n: int, k: int) -> List[List[int]]:
        def backtrack(start = 1, curr = []):
            if len(curr) == k:
                ans.append(curr[:])
            else:
                for i in range(start, n + 1):
                    curr.append(i)
                    backtrack(i + 1, curr)
                    curr.pop()

        ans = []
        backtrack(1, [])
        return ans
```

