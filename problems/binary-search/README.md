# Binary Search 二分搜索

二分搜索的要點：

1. 確立邊界，這樣會導致我們是在閉區間或是非閉區間搜尋
   1. 左側的邊界，ex: 0 or 1？
   2. 右側的邊界，ex: `len(nums)` or `len(nums) - 1`
2. 循環條件的終止，ex: `while left <= right` or `while left < right`

### Binary Search

```python
def binarySearch(nums: List[int], target: int) -> int:
    left = 0
    right = len(nums) - 1
    while left <= right:
        mid = left + (right - left) // 2
        if nums[mid] == target:
            return mid
        elif nums[mid] < target:
            left = mid + 1
        elif nums[mid] > target:
            right = mid - 1
    return -1
```

### Find Left Bound

```python
def findLeftBound(nums: List[int], target: int) -> int:
    left = 0
    right = len(nums)
    while left < right:
        mid = left + (right - left) // 2
        if nums[mid] == target:
            right = mid
        elif nums[mid] < target:
            left = mid + 1
        elif nums[mid] > target:
            right = mid
    return left
```

```python
def findLeftBound(nums: List[int], target: int) -> int:
    left = 0
    right = len(nums) - 1
    while left <= right:
        mid = left + (right - left) // 2
        if nums[mid] == target:
            right = mid - 1
        elif nums[mid] < target:
            left = mid + 1
        elif nums[mid] > target:
            right = mid - 1
    if left >= len(nums) or nums[left] != target:
        return -1
    return left
```

### Find Right Bound

```python
def findRightBound(nums: List[int], target: int) -> int:
    left = 0
    right = len(nums)
    while left < right:
        mid = left + (right - left) // 2
        if nums[mid] == target:
            left = mid + 1
        elif nums[mid] < target:
            left = mid + 1
        elif nums[mid] > target:
            right = mid
    return right - 1
```

```python
def findRightBound(nums: List[int], target: int) -> int:
    left = 0
    right = len(nums) - 1
    while left <= right:
        mid = left + (right - left) // 2
        if nums[mid] == target:
            left = mid + 1
        elif nums[mid] < target:
            left = mid + 1
        elif nums[mid] > target:
            right = mid - 1
    if right < 0 or nums[right] != target:
        return -1
    return right
```



