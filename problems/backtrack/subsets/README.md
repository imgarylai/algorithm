# 78. Subsets

[78. Subsets](https://leetcode.com/problems/subsets/)

我們需要一個長度來終結 backtrack ，所以多傳了一個參數 k 做為判斷 Backtrack 終止的條件。

```python
class Solution:
    def subsets(self, nums: List[int]) -> List[List[int]]:
        ans = []
        n = len(nums)
        def backtrack(k, curr, start):
            if len(curr) == k:
                ans.append(list(curr))
                return
            for i in range(start, n):
                curr.append(nums[i])
                backtrack(k, curr, i + 1)
                curr.pop()
        
        for k in range(len(nums) + 1):
            backtrack(k, [], 0)
        return ans
```

