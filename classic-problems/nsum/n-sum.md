# n Sum

[15. 3 Sum](https://leetcode.com/problems/3sum/)

[18. 4 Sum](https://leetcode.com/problems/4sum/)

於是這樣就可以開始擴展當 `n > 2` 的時候， 該怎麼辦呢？

* 當 `n == 1` 的時候，沒有所謂的總和問題，所以答案為**空集合。**
* 當 `n == 2` 的時候，就是所謂的 **2 Sum** ，可以透過上方的方式找到
* 當 `n == 3` 的時候，是不是可以把設定的目標先剪去第一個陣列中的第 `i` 個數字，得到一個新目標，接著在剩下的兩個陣列中，用新的目標找 **2 Sum** 。
* ...
* 當 `n == k` 的時候，就可以推導出，先將目標減去第一個陣列中的第 `i` 個數字，得到一個新目標後，在接下來的 k - 1 個陣列中，找出 **k-1 Sum** 。

所以我們就找到了基本情況， `n == 1` 與 `n == 2`，並且可以透過遞迴的方式來找出 nSum 。

```python
class Solution:
    def twoSum(self, nums: List[int], start: int, target: int) -> List[List[int]]:
        left = start
        right = len(nums) - 1
        res = []
        while left < right:
            total = nums[left] + nums[right]
            leftVal = nums[left]
            rightVal = nums[right]
            if total < target:
                left += 1
            elif total > target:
                right -= 1
            else: # s == target
                res.append([nums[left], nums[right]]) 
                while (left < right and leftVal == nums[left]):
                    left += 1
                while (left < right and rightVal == nums[right]):
                    right -= 1
        return res

    def nSum(self, nums, n, start, target):
        size = len(nums)
        res = []
        if n < 2 or size < n:
            return res
        if n == 2:
            return self.twoSum(nums, start, target)
        else:
            i = start
            while i < size:
                tuples = self.nSum(nums, n - 1, i + 1, target - nums[i])
                for tup in tuples:
                    tup.append(nums[i])
                    res.append(tup)
                while i < size - 1 and nums[i] == nums[i + 1]:
                    i += 1
                i += 1
        return res


    def fourSum(self, nums: List[int], target: int) -> List[List[int]]:
        nums.sort()
        return self.nSum(nums, 4, 0, target)
```

