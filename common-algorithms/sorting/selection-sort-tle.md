# Selection Sort \(TLE\)

```python
class Solution:
    def sortArray(self, nums: List[int]) -> List[int]:
        return self.selection_sort(nums)

    def selection_sort(self, nums):
        for i in range(len(nums)):
            _min = min(nums[i:])
            min_index = nums[i:].index(_min)
            nums[i + min_index] = nums[i]
            nums[i] = _min
        return nums
```

