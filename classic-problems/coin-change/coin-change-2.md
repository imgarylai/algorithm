# 518. Coin Change 2

[518. Coin Change 2](https://leetcode.com/problems/coin-change-2/)

[322. Coin Change](coin-change.md) 是找出最少硬幣的組合，這個題目是找出總共有幾種組合，其選擇的方式是類似的，就是要不斷的選擇，並且對目標減去選擇的硬幣的價值。

不過這裡有一個地方要優化，那就是對於目標值為 `5` 來說，選擇 `[2, 2, 1], [2, 1, 2], [1, 2, 2]` 都是一樣的情況。所以這時候可以針對此情況來優化，例如一開始就一直選小的硬幣，如果我開始選大的硬幣，我就要不斷地選更大的硬幣，策略性地去做選擇。

時間複雜度和上一題相同。

```python
class Solution:
    def change(self, amount: int, coins: List[int]) -> int:

        ans = []
        memo = {}
        def helper(target, index):
            if (target, index) in memo:
                return memo[(target, index)]
            if target < 0:
                memo[(target, index)] = 0
            elif target == 0:
                memo[(target, index)] = 1
            else:
                count = 0
                for i in range(index, len(coins)):
                    coin = coins[i]
                    count += helper(target - coin, i)
                memo[(target, index)] = count
            return memo[(target, index)]

        return helper(amount, 0)
```

```python
class Solution:
    def change(self, amount: int, coins: List[int]) -> int:
        dp = [0] * (amount + 1)
        dp[0] = 1

        for coin in coins:
            for i in range(coin, amount + 1):
                dp[i] += dp[i - coin]
        return dp[amount]
```

