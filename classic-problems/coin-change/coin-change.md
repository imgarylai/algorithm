# 322. Coin Change

[322. Coin Change](https://leetcode.com/problems/coin-change/)

### 自頂向下

選擇硬幣的過程就像是一個遞迴樹的過程，每次我選一枚硬幣後，目標就會減少該硬幣的價值的量，如果一直到目標為零的時候，就沒有任何選擇需要選。

但這個題目存在著許多的重複子問題，所以可以透過記憶法的方式優化。

時間複雜度為最差的情況是我們需要走遍 `amount` ，接著做 `len(n)` 次的遍歷： $$O( \text{amount} * \text{len(n}))$$ 

```python
class Solution:
    def coinChange(self, coins: List[int], amount: int) -> int:
        
        @lru_cache(None)
        def helper(target):
            if target < 0:
                return -1
            if target == 0:
                return 0
            else:
                ans = float('inf')
                for coin in coins:
                    res = helper(target-coin)
                    if res >= 0 and res < ans:
                        ans = 1 + res
                return -1 if ans == float('inf') else ans
        return helper(amount)
```

### 自底向上

```python
class Solution:
    def coinChange(self, coins: List[int], amount: int) -> int:
        dp = [float('inf')] * (amount + 1)
        dp[0] = 0
        for i in range(len(dp)):
            for coin in coins:
                if i - coin >= 0:
                    dp[i] = min(dp[i], 1 + dp[i-coin])

        return -1 if dp[amount] == float('inf') else dp[amount]
```

