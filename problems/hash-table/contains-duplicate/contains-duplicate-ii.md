# 219. Contains Duplicate II

[219. Contains Duplicate II](https://leetcode.com/problems/contains-duplicate-ii/)

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

