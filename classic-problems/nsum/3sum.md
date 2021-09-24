# 15. 3Sum

[15. 3 Sum](https://leetcode.com/problems/3sum/)

```python
# target: 0

# [-1, -1, 2, -1]
# -> [-1, -1, 2], [-1, 2, -1] choose one

# Approach 
#     For each number
#         1. target - nums[0]: 1
#         2. Find two number in the rest of array which sum to -1
#             -> Become a smaller question. it is 2 sum    

# Approach for twoSum:
#     First sort the array. 
#     We can use binary search to find the solution. 
#     [-1, -1, 0, 1, 2] target = 0
#     left: -1, right: 2 -> 1 and 1 > 0 the sum is too large
#     left: -1, right: 1 -> 0 we found the target 
    
            
class Solution:
    def twoSum(self, nums: List[int], target) -> List[List[int]]:
        left = 0
        right = len(nums) - 1
        res = []
        while left < right:
            leftNum = nums[left]
            rightNum = nums[right]
            total = leftNum + rightNum
            if total == target:
                res.append([leftNum, rightNum])
                while left < right and leftNum == nums[left]:
                    left += 1
                while left < right and rightNum == nums[right]:
                    right -= 1
            elif total < target:
                left += 1
            elif total > target:
                right -= 1
        return res
        
        
    def threeSum(self, nums: List[int]) -> List[List[int]]:
        
        res = []
        nums.sort()
        if len(nums) <= 2:
            return []
        i = 0
        while i < len(nums):
            num = nums[i]
            candidates = self.twoSum(nums[i+1:], 0 - num)
            for candidate in candidates:
                candidate.append(num)
                res.append(candidate)
            i += 1
            while i < len(nums) and num == nums[i]:
                i += 1
                
        return res
        
```

