# 219. Contains Duplicate II

[219. Contains Duplicate II](https://leetcode.com/problems/contains-duplicate-ii/)

這一題和 2 Sum 的原理有點像，我們需要用到 Table 來記憶元素出現的位置，不過這個題目只需要記憶著每個字元最後出現的位置即可。

```python
class Solution:
    def containsNearbyDuplicate(self, nums: List[int], k: int) -> bool:
        table = {}

        for i in range(len(nums)):
            num = nums[i]
            if num in table:
                if abs(i - table[num]) <= k:
                    return True
            table[num] = i

        return False
```

