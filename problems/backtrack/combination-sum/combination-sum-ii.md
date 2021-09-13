# 40. Combination Sum II

[40. Combination Sum II](https://leetcode.com/problems/combination-sum-ii/)

這題是以下兩題的總和，

1. 像是 Subsets II 一樣，如果有重複的答案我們不要。
2. 和 Combination Sum 不同的是，每一個數字有使用的上限。

{% page-ref page="./" %}

{% page-ref page="../subsets/subsets-ii.md" %}

```python
class Solution:
    def combinationSum2(self, candidates: List[int], target: int) -> List[List[int]]:
        ans = []
        candidates.sort()
        def backtrack(curr, target, start, counter):
            if target == 0:
                ans.append(list(curr))
                return
            elif target < 0:
                return
            else:
                for i in range(start, len(candidates)):
                    if i > start and candidates[i] == candidates[i -1]:
                        continue
                    curr.append(candidates[i])
                    counter[candidates[i]] -= 1
                    backtrack(curr, target - candidates[i], i + 1, counter)
                    counter[candidates[i]] += 1
                    curr.pop()

        backtrack([], target, 0, Counter(candidates))
        return ans
```

