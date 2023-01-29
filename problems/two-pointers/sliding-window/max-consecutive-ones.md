# 485. Max Consecutive Ones

[485. Max Consecutive Ones](https://leetcode.com/problems/max-consecutive-ones/)

```python
class Solution:
    def findMaxConsecutiveOnes(self, nums: List[int]) -> int:
        res = 0
        prev = 0
        for curr in range(len(nums)):
            if nums[curr] == 1:
                res = max(res, curr - prev + 1)
            else:
                prev = curr + 1
        return res
```

