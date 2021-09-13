# 278. First Bad Version

[278. First Bad Version](https://leetcode.com/problems/first-bad-version/)

如果中間值是錯誤的版本，代表最早的錯誤版本在左區間

如果中間值是正確的版本，代表最早的錯誤版本在右區間

```python
# The isBadVersion API is already defined for you.
# @param version, an integer
# @return an integer
# def isBadVersion(version):

class Solution:
    def firstBadVersion(self, n):
        """
        :type n: int
        :rtype: int
        """
        left = 1
        right = n
        while left < right:
            mid = left + (right - left) // 2
            if isBadVersion(mid):
                right = mid
            else:
                left = mid + 1
        
        return left
```

