# 398. Random Pick Index

[398. Random Pick Index](https://leetcode.com/problems/random-pick-index/)

```python
class Solution:

    def __init__(self, nums: List[int]):
        self.nums = nums
        
    def pick(self, target: int) -> int:
        k = 1
        res = None
        
        for i, n in enumerate(self.nums):
            if n == target:
                if random.random() < 1/k:
                    res = i
                k += 1
        return res
        


# Your Solution object will be instantiated and called as such:
# obj = Solution(nums)
# param_1 = obj.pick(target)
```

