# 1004. Max Consecutive Ones III

[1004. Max Consecutive Ones III](https://leetcode.com/problems/max-consecutive-ones-iii/)

```python
class Solution:
    def longestOnes(self, nums: List[int], k: int) -> int:
        slow, fast, zeros, ans = 0, 0, 0, 0

        while fast < len(nums):
            if nums[fast] == 0:
                zeros += 1

            if zeros > k:
                if nums[slow] == 0:
                    zeros -= 1
                slow += 1

            ans = max(ans, fast - slow + 1)
            fast += 1

        return ans
```

