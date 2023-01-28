# 259. 3Sum Smaller

[259. 3Sum Smaller](https://leetcode.com/problems/3sum-smaller/)

```python
class Solution:        
    def threeSumSmaller(self, nums: List[int], target: int) -> int:
        count = 0
        nums.sort()
        for i in range(len(nums)):
            num = nums[i]
            left = i + 1
            right = len(nums) - 1
            while left < right:
                threeSum = num + nums[left] + nums[right]
                if threeSum < target:
                    count += right - left
                    left += 1
                else:
                    right -= 1
                    
        return count
```

