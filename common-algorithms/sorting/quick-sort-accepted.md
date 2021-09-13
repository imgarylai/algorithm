# Quick Sort \(Accepted\)

```python
class Solution:
    def sortArray(self, nums: List[int]) -> List[int]:
        return self.quick_sort(nums)
    
    
    def quick_sort(self, nums):
        if not nums: return nums # empty sequence case
        pivot = nums[random.choice(range(0, len(nums)))]
        head = []
        middle = []
        tail = []
        for num in nums:
            if num < pivot: head.append(num)
            elif num > pivot: tail.append(num)
            else: middle.append(num)
        return self.quick_sort(head) + middle + self.quick_sort(tail)
```

