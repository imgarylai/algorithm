# 打亂陣列內的元素

[384. Shuffle ans Array](https://leetcode.com/problems/shuffle-an-array/)

```python
class Solution:

    def __init__(self, nums: List[int]):
        self.nums = nums
        self.original = list(nums)

    def reset(self) -> List[int]:
        """
        Resets the array to its original configuration and return it.
        """
        self.nums = self.original
        self.original = list(self.original)
        return self.nums
        

    def shuffle(self) -> List[int]:
        """
        Returns a random shuffling of the array.
        """
        for i in range(len(self.nums)):
            idx = random.randrange(i, len(self.nums))
            self.nums[i], self.nums[idx] = self.nums[idx], self.nums[i]
        return self.nums
```



* [Fisher–Yates shuffle](https://en.wikipedia.org/wiki/Fisher%E2%80%93Yates_shuffle)

