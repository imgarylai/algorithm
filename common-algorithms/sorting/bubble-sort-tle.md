# Bubble Sort \(TLE\)

```python
class Solution:
    def sortArray(self, nums: List[int]) -> List[int]:
        return self.bubble_sort(nums)

    def bubble_sort(self, nums):
        n = len(nums)
        for i in range(n):
            for j in range(0, n - i - 1):
                if nums[j] > nums[j + 1]:
                    nums[j], nums[j + 1] = nums[j + 1], nums[j]
```

