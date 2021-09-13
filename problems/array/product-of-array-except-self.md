# 238. Product of Array Except Self

[238. Product of Array Except Self](https://leetcode.com/problems/product-of-array-except-self/)

```python
class Solution:
    def productExceptSelf(self, nums: List[int]) -> List[int]:
        length = len(nums)
        
        left2right = [0] * length
        right2left = [0] * length
        
        ans = [0] * length
        
        left2right[0] = 1
        for i in range(1, length):
            left2right[i] = left2right[i - 1] * nums[i - 1]
        
        right2left[length - 1] = 1
        for i in reversed(range(length-1)):
            right2left[i] = right2left[i + 1] * nums[i + 1]
        
        for i in range(length):
            ans[i] = left2right[i] * right2left[i]
        
        return ans
```



