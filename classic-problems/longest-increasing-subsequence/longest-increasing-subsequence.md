# 300. Longest Increasing Subsequence

[300. Longest Increasing Subsequence](https://leetcode.com/problems/longest-increasing-subsequence/)

這一個題目是比較容易用直覺判斷出是動態規劃的題目，難的地方是他的動態轉移方程。

首先先想`dp[i]` 要記錄的是什麼？是如果到 `num[i]` 這個位置時， 最長遞增子序列的長度。

例如：

```text
# 題目
nums = [0,1,0,3,2,3]
# 當 i == 1 時
dp[i] => 2
```

基本的型態會是什麼？最長的遞增子序列就只有自己而已，那時候 dp\[i\] 就會是 1 。

這時候我們想要知道的就是 當我們已經知道 `dp[0..i-1]` 的所有數值時，要怎麼求 `dp[i]` 的數值？

分兩個步驟想，第一個步驟是，我們要找到最長遞增子序列，和當前 `nums[i]` 有用的，只有**在我前面，比我小的數字**才有用，因為比他大的，都不可能增加最長遞增子序列的長度，所以我們要去找 `nums[0..i-1]`中 ，比 `nums[i]` 還小的數字。

找到之後，就是第二個步驟，這些比 `nums[i]` 還小的數字，**他們當時的最長遞增子序列的長度為何？**候選人可能有很多，但是我們知道一定是要找最長的那個，這時候就可以更新我們自己的最長遞增子序列的長度 `dp[i]` 。更新的方式如下：

```text
dp[i] = max(dp[i], dp[j] + 1) 
# j is the index which is smaller than i and contributes the longest increasing subsequence.
```

最後的答案。

```python
class Solution:
    def lengthOfLIS(self, nums: List[int]) -> int:
        dp = [1] * len(nums)

        for i in range(1, len(nums)):
            for j in range(i):
                if nums[j] >= nums[i]:
                    continue
                else:
                    dp[i] = max(dp[i], dp[j]+1)

        return max(dp)
```

時間複雜度： $$O(n^2)$$

## 補充

這個題目其實有一個更快的解法，時間複雜度只要 $$O(nlogn)$$ ，是使用一個叫做[耐心排序\(Patience sorting\)](https://en.wikipedia.org/wiki/Patience_sorting)的方法。

講解得最好的講義：[https://www.cs.princeton.edu/courses/archive/spring13/cos423/lectures/LongestIncreasingSubsequence.pdf](https://www.cs.princeton.edu/courses/archive/spring13/cos423/lectures/LongestIncreasingSubsequence.pdf)

```python
class Solution:
    def lengthOfLIS(self, nums: List[int]) -> int:
        piles = [] # 牌堆，一開始沒有牌堆

        # 開始整理撲克牌
        for i in range(len(nums)):
            # 目前要整理的牌
            card = nums[i]

            # 我有哪些排堆可以整理，用二分搜索的方式來整理
            left, right = 0, len(piles) - 1
            while left <= right:
                mid = left + (right - left) // 2
                # 如果這個牌堆最上面的撲克牌比我的牌大，那我要往左邊找，而且要盡可能地往左邊放
                if piles[mid][-1] >= card:
                    right = mid - 1
                # 如果這個牌堆最上面的撲克牌比我的牌小，那我要往右邊找
                else: # piles[mid][-1] < card:
                    left = mid + 1

            # 沒有地方可以放，新增一個牌堆
            if left == len(piles):
                piles.append([])
            # 把撲克牌放入牌堆
            piles[left].append(card)
        return len(piles)
```

上面這個算法如果有幾個牌堆，就代表了最長**「遞增」**子序列的值，如果要找最長**「遞減」**子序列，就要找這些牌堆中，哪個牌堆的長度最長。

