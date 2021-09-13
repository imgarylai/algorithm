# 154. Find Minimum in Rotated Sorted Array II

[154. Find Minimum in Rotated Sorted Array II](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array-ii/)

如果中間的值比最右邊的大，那代表最小值在右區間

如果中間的值比最右邊的小，那代表最小值在左區間

但是因為有重複的值，所以遇到重複的時候，右邊邊界縮小一

為什麼不能左邊界加一？因為我們是要找最小值，如果左邊界加一可能會把最小值給跳過了。

```python
class Solution:
    def findMin(self, nums: List[int]) -> int:
        left = 0
        right = len(nums) - 1

        while left < right:
            mid = left + (right - left) // 2
            if nums[mid] > nums[right]:
                left = mid + 1
            elif nums[mid] < nums[right]:
                right = mid
            else:
                right -= 1

        return nums[left]
```

雖然這題是 Binary Search 做，可是時間複雜度有可能是 $$O(N)$$ 。

