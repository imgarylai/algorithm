# Merge Sort \(Accepted\)

```python
class Solution:
    def sortArray(self, nums: List[int]) -> List[int]:
        return self.merge_sort(nums)
        
    def merge_sort(self, nums: List[int]) -> List[int]:
        L = len(nums)
        if L <= 1:
            return nums
        m = L //2
        left_list = self.merge_sort(nums[:m])
        right_list = self.merge_sort(nums[m:])
        return self.merge(left_list, right_list)
    
    def merge(self, left_list: List[int], right_list: List[int]) -> List[int]:
        left_cursor = 0
        right_cursor = 0
        res = []
        while left_cursor < len(left_list) and right_cursor < len(right_list):
            if left_list[left_cursor] < right_list[right_cursor]:
                res.append(left_list[left_cursor])
                left_cursor += 1
            else:
                res.append(right_list[right_cursor])
                right_cursor += 1
        
        res.extend(left_list[left_cursor:])
        res.extend(right_list[right_cursor:])
        return res
```

