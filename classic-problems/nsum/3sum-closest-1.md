# 16. 3Sum Closest

[16. 3Sum Closest](https://leetcode.com/problems/3sum-closest/)

```python
class Solution:
    def threeSumClosest(self, nums: List[int], target: int) -> int:
        nums.sort()
        diff = float('inf')
        for i in range(len(nums)):
            left = i + 1
            right = len(nums) - 1
            while left < right:
                threeSum = nums[i] + nums[left] + nums[right]
                if abs(target - threeSum) < abs(diff):
                    diff = target - threeSum
                if threeSum < target:
                    left += 1
                else:
                    right -= 1
            if diff == 0:
                break
                
        return target - diff
```

