# 1089. Duplicate Zeros

[1089. Duplicate Zeros](https://leetcode.com/problems/duplicate-zeros/)

```python
class Solution:
    def duplicateZeros(self, arr: List[int]) -> None:
        """
        Do not return anything, modify arr in-place instead.
        """
        i = 0
        n = len(arr)
        while i < n:
            if arr[i] == 0:
                arr[::] = arr[:i] + [0] + arr[i:n-1]
                i += 2
            else:
                i += 1
```

