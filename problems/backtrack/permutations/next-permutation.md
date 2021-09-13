# 31. Next Permutation

[31. Next Permutation](https://leetcode.com/problems/next-permutation/)

我的第一個想法，但是超時

```python
class Solution:
    def nextPermutation(self, nums: List[int]) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        sortedNums = sorted(nums)
        res = []
        def backtrack(curr, counter):
            if len(curr) == len(sortedNums):
                res.append(list(curr))
                return
            else:
                for num in counter:
                    if counter[num] > 0:
                        counter[num] -= 1
                        curr.append(num)
                        backtrack(curr, counter)
                        counter[num] += 1
                        curr.pop()

        backtrack([], Counter(sortedNums))
        i = 0
        while i < len(res):
            if ''.join(map(str, res[i])) == ''.join(map(str, nums)):
                break
            i += 1
        if i == len(res) - 1: 
            nums[::] = res[0]
        else: 
            nums[::] = res[i+1]
```

