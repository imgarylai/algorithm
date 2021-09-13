# 39. Combination Sum

[39. Combination Sum](https://leetcode.com/problems/combination-sum/)

這個題目也是窮舉題目，我們每次都從最小的數字開始拿，慢慢的往上加，如果說最後沒辦法湊到結果，就把最後一個數字拿掉，再看看大一點的數字可不可以到目標。有一點像是換錢幣的題目。

```python
class Solution:
    def combinationSum(self, candidates: List[int], target: int) -> List[List[int]]:
        ans = []
        def backtrack(curr, target):
            if target == 0:
                ans.append(list(curr))
            if target < 0:
                return
            for candidate in candidates:
                if len(curr) > 0:
                    # 確保只拿比自己大或是相等的數字
                    if candidate < curr[-1]:
                        continue
                curr.append(candidate)
                backtrack(curr, target - candidate)
                curr.pop()
        backtrack([], target)
        return ans
```

也可以透過傳指針的位置來判斷現在應該要從哪裡開始找

```python
class Solution:
    def combinationSum(self, candidates: List[int], target: int) -> List[List[int]]:
        ans = []
        def backtrack(curr, remaining, start):
            if remaining == 0:
                ans.append(list(curr))
                return
            if remaining < 0:
                return
            for i in range(start, len(candidates)):
                candidate = candidates[i]
                curr.append(candidate)
                backtrack(curr, remaining - candidate, i)
                curr.pop()
        backtrack([], target, 0)
        return ans
```

