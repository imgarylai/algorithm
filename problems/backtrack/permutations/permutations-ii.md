# 47. Permutations II

[47. Permutations II](https://leetcode.com/problems/permutations-ii/)

有重複的數字出現，要去記錄使用的次數

```python
class Solution:
    def permuteUnique(self, nums: List[int]) -> List[List[int]]:
        res = []
        def backtrack(curr, counter):
            if len(curr) == len(nums):
                res.append(list(curr))
                return
            for num in counter:
                if counter[num] > 0:
                    counter[num] -= 1
                    curr.append(num)
                    backtrack(curr, counter)
                    counter[num] += 1
                    curr.pop()
        backtrack([], Counter(nums))
        return res
```

