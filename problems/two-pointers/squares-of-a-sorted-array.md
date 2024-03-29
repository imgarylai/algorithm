# 977. Squares of a Sorted Array

[997. Squares of a Sorted Array](https://leetcode.com/problems/squares-of-a-sorted-array/)

題目的陣列有排序好，不過從陣列的兩側，我們只知道目前的最大值是多少，所以雖然題目問的是從小排到大，我們可以先把陣列求大排到小，再反序就好。

透過兩個指針可以判斷左邊或是右邊的元素要先放進來，我們要確定如果有負值的絕對值比較大，我們就先加入。

```python
class Solution:
    def sortedSquares(self, nums: List[int]) -> List[int]:
        left = 0
        right = len(nums) - 1
        res = []
        while left <= right:
            if abs(nums[left]) > abs(nums[right]):
                res.append(nums[left] ** 2)
                left += 1
            else:
                res.append(nums[right] ** 2)
                right -= 1

        return res[::-1]
```

