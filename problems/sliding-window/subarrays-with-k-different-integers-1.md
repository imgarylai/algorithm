# 992. Subarrays with K Different Integers

[992. Subarrays with K Different Integers](https://leetcode.com/problems/subarrays-with-k-different-integers/)

```python
class Solution:
    def subarraysWithKDistinct(self, nums: List[int], k: int) -> int:
        def atMostK(k):
            count = collections.Counter()
            res = 0
            slow = 0
            for fast in range(len(nums)):
                if count[nums[fast]] == 0: k -= 1
                count[nums[fast]] += 1
                while k < 0:
                    count[nums[slow]] -= 1
                    if count[nums[slow]] == 0: k += 1
                    slow += 1
                res += fast - slow + 1
            return res
        return atMostK(k) - atMostK(k - 1)
```

