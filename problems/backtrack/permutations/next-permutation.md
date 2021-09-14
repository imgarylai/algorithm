# 31. Next Permutation

[31. Next Permutation](https://leetcode.com/problems/next-permutation/)

題目是給定一個數字，要使用這個數字有使用到的數字，並透過排列組合，找到下一個排列組合比現在這個數字還大，可是卻是所有可行的排列組合中最小的，如果說現在的這個數字已經是排列組合中最大的數字，那我們就回傳排列組合中最小的數字。這個排列也可以稱做一種字典排列。

我的第一個直覺想法是，既然是排列組合題目，那我就把所有的排列組合窮舉出來，並且由小到大的排序，找出哪個數字和目前的數字相同，下一個數字就會是字典數了，當然如果是最大的數字，那就返回最小的數，題目還有要求要只在記憶體修改，那是這個並不是太困難的事情。

### 回溯法

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

但是我的做法時間複雜度非常高，會超時。

### 解法

這個解法只針對這個題目，不過因為這個題目是 Google 的高頻考題，所以我還是把這個題目放到了筆記之中。

