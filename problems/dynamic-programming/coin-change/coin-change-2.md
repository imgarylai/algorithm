# 518. Coin Change 2

[518. Coin Change 2](https://leetcode.com/problems/coin-change-2/)

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

