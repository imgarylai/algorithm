# 704. Binary Search

[704. Binary Search](https://leetcode.com/problems/binary-search/)

```python
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        left = 0
        right = len(nums) - 1
        
        while left <= right:
            mid = left + (right - left) // 2
            if nums[mid] == target:
                return mid
            if nums[mid] > target:
                right = mid - 1
            if nums[mid] < target:
                left = mid + 1
        
        return -1
```

```python
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        left = 0
        right = len(nums) - 1
        
        def binarySearch(left, right):
            if left > right:
                return -1
            mid = left + (right - left) // 2
            if nums[mid] == target:
                return mid
            if nums[mid] > target:
                return binarySearch(left, mid - 1)
            if nums[mid] < target:
                return binarySearch(mid + 1, right)
        
        return binarySearch(left, right)
```

