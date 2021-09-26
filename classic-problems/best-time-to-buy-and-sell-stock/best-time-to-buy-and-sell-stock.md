# 121. Best Time to Buy and Sell Stock

[121. Best Time to Buy and Sell Stock](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/)

不斷的找出前低點，並且看看目前的價格是不是高點，當前的價格減去之前的最低點比當前的最高獲利高，那就代表我們有更好的獲利，更新最高獲利的數值。

```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        if len(prices) < 2:
            return 0
        min_cost = prices[0]
        max_profit = 0
        for price in prices:
            min_cost = min(min_cost, price)
            max_profit = max(max_profit, price - min_cost)
        return max_profit
```

