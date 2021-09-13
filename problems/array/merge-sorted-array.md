# 88. Merge Sorted Array

[88. Merge Sorted Array](https://leetcode.com/problems/merge-sorted-array/)

```python
class Solution:
    def merge(self, nums1: List[int], m: int, nums2: List[int], n: int) -> None:
        """
        Do not return anything, modify nums1 in-place instead.
        """
        nums1Copy = nums1[:m]

        i = 0
        j = 0
        k = 0

        while i < m and j < n:
            if nums1Copy[i] < nums2[j]:
                nums1[k] = nums1Copy[i]
                i += 1
            else:
                nums1[k] = nums2[j]
                j += 1
            k += 1

        if i == m:
            nums1[k:] = nums2[j:]
        if j == n:
            nums1[k:] = nums1Copy[i:]
```

