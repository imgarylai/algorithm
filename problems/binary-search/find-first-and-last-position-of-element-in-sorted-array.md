# 34. Find First and Last Position of Element in Sorted Array

[34. Find First and Last Position of Element in Sorted Array](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/)

這一題是一個非常好的二分搜索的尋找左邊界與右邊界的問題。

```python
class Solution:
    def findLeftBound(self, nums: List[int], target: int) -> int:
        left = 0
        right = len(nums) - 1
        while left <= right:
            mid = left + (right - left) // 2
            if nums[mid] == target:
                right = mid - 1
            elif nums[mid] < target:
                left = mid + 1
            elif nums[mid] > target:
                right = mid - 1
        if left >= len(nums) or nums[left] != target:
            return -1
        return left
    def findRightBound(self, nums: List[int], target: int) -> int:
        left = 0
        right = len(nums) - 1
        while left <= right:
            mid = left + (right - left) // 2
            if nums[mid] == target:
                left = mid + 1
            elif nums[mid] < target:
                left = mid + 1
            elif nums[mid] > target:
                right = mid - 1
        if right < 0 or nums[right] != target:
            return -1
        return right
    def searchRange(self, nums: List[int], target: int) -> List[int]:  
        left_bound = self.findLeftBound(nums, target)
        right_bound = self.findRightBound(nums, target)
        return [left_bound, right_bound]
```

```python
class Solution:
    def searchRange(self, nums: List[int], target: int) -> List[int]:  

        left = 0
        right = len(nums) - 1
        while left <= right:
            mid = left + (right - left) // 2
            if nums[mid] >= target:
                right = mid - 1
            elif nums[mid] < target:
                left = mid + 1

        left_bound = -1 if (left >= len(nums) or nums[left] != target) else left

        left = 0
        right = len(nums) - 1
        while left <= right:
            mid = left + (right - left) // 2
            if nums[mid] <= target:
                left = mid + 1
            if nums[mid] > target:
                right = mid - 1

        right_bound = -1 if (right < 0 or nums[right] != target) else right

        return [left_bound, right_bound]
```

