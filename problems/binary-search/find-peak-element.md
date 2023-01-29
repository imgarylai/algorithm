# 162. Find Peak Element

[162. Find Peak Element](https://leetcode.com/problems/find-peak-element/)

如果下一個值比現在這個值大，代表可以繼續往上爬

如果下一個值比現在這個值小，代表頂峰在後面

題目有可能有不只一個頂峰，但是題目說可以回傳任意一個頂峰即可。

```python
class Solution:
    def findPeakElement(self, nums: List[int]) -> int:
        left = 0
        right = len(nums) - 1
        while left < right:
            mid = left + (right - left) // 2
            if nums[mid] < nums[mid + 1]:
                left = mid + 1
            else:
                right = mid
        return left
```

