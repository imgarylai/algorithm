# 18. 4Sum

[18. 4 Sum](https://leetcode.com/problems/4sum/)

```python
class Solution:
    def twoSum(self, nums: List[int], start: int, target: int) -> List[List[int]]:
        left = start
        right = len(nums) - 1
        res = []
        while left < right:
            total = nums[left] + nums[right]
            leftVal = nums[left]
            rightVal = nums[right]
            if total < target:
                left += 1
            elif total > target:
                right -= 1
            else: # s == target
                res.append([nums[left], nums[right]]) 
                while (left < right and leftVal == nums[left]):
                    left += 1
                while (left < right and rightVal == nums[right]):
                    right -= 1
        return res
    
    def nSum(self, nums, n, start, target):
        size = len(nums)
        res = []
        if n < 2 or size < n:
            return res
        if n == 2:
            return self.twoSum(nums, start, target)
        else:
            i = start
            while i < size:
                num = nums[i]
                tuples = self.nSum(nums, n - 1, i + 1, target - nums[i])
                for tup in tuples:
                    tup.append(nums[i])
                    res.append(tup)
                i += 1
                while i < size - 1 and nums[i] == num:
                    i += 1
        return res
                
    
    def fourSum(self, nums: List[int], target: int) -> List[List[int]]:
        nums.sort()
        return self.nSum(nums, 4, 0, target)
```

