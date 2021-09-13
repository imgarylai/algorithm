# 46. Permutations

[46. Permutations](https://leetcode.com/problems/permutations/)

排列組合，要確保已經使用過的數字不要再使用

```python
class Solution:
    def permute(self, nums: List[int]) -> List[List[int]]:
        res = []
        def backtrack(curr):
            if len(curr) == len(nums):
                res.append(list(curr))
                return
            for num in nums:
                if num in curr:
                    continue
                curr.append(num)
                backtrack(curr)
                curr.pop()
        backtrack([])
        return res
```

