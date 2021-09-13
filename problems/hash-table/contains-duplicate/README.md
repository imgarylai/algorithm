# 217. Contains Duplicate

[217. Contains Duplicate](https://leetcode.com/problems/contains-duplicate/)

```python
class Solution:
    def containsDuplicate(self, nums: List[int]) -> bool:
        S = set(nums)
        return len(S) != len(nums)
```



