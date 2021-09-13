# 852. Peak Index in a Mountain Array

[852. Peak Index in a Mountain Array](https://leetcode.com/problems/peak-index-in-a-mountain-array/)

1. 在閉區間搜尋
2. 從中間開始找
   1. 如果下一個數字比現在的大，向右逼近
   2. 如果下一個數字比現在小或是一樣，向左逼近



```python
class Solution:
    def peakIndexInMountainArray(self, arr: List[int]) -> int:
        left = 0
        right = len(arr) - 1
        while left < right:
            mid = left + (right - left) // 2
            if arr[mid] < arr[mid + 1]:
                left = mid + 1
            else:
                right = mid
        return left
```

