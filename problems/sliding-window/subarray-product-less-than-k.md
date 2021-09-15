# 713. Subarray Product Less Than K

[713. Subarray Product Less Than K](https://leetcode.com/problems/subarray-product-less-than-k/)

這一題很容易就可以想到是滑動窗口的題目，滑動窗口的條件判斷很簡單，如果目前的積還小於 `k` ，那就繼續增大窗口，當目前的積大於 `k` 時縮小窗口。

困難是在於滑動窗口後怎麼樣去計算到底有多少個子陣列滿足題目的條件？

```text
nums = [10,5,2,6]
[10] 1
[10, 5] 2
[5, 2] 2
[5, 2, 6] 3
```

```python
class Solution:
    def numSubarrayProductLessThanK(self, nums: List[int], k: int) -> int:
        if k <= 1:
            return 0
        fast = 0
        slow = 0
        res = 1
        ans = 0
        while fast < len(nums):
            num = nums[fast] 
            fast += 1
            res *= num
            while res >= k:
                num = nums[slow]
                slow += 1
                res //= num
            ans += fast - slow
                    
        return ans
```

