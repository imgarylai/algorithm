# 673. Number of Longest Increasing Subsequence

[673. Number of Longest Increasing Subsequence](https://leetcode.com/problems/number-of-longest-increasing-subsequence/)

## Prerequisite

{% page-ref page="longest-increasing-subsequence.md" %}

核心和 [300. Longest Increasing Subsequence](longest-increasing-subsequence.md) 一樣，不過除了要記錄的是當前的最長上升子序列的長度外，要外去記憶有多少種路徑可以到，可以用 `tuple` 記錄`（當前最長上升子序列的長度，前面有幾種路徑）` 。

```python
class Solution:
    def findNumberOfLIS(self, nums: List[int]) -> int:
        dp = [(1, 1) for _ in range(len(nums))]
        LIS = 1
        for i in range(1, len(nums)):
            curr, count = 1, 0
            # 先計算出當前的最長遞增子序列的最大長度為何
            for j in range(i):
                if nums[j] < nums[i]:
                    curr = max(curr, dp[j][0] + 1)
            LIS = max(LIS, curr)

            # 再去累加有哪些路徑可以到
            for j in range(i):
                if nums[j] < nums[i] and dp[j][0] == curr - 1:
                    count += dp[j][1]

            # 更新當前的最長遞增子序列和路徑組合
            dp[i] = (curr, max(count, dp[i][1]))

        ans = 0
        for item in dp:
            curr, count = item
            if curr == LIS:
                ans += count
        return ans
```

