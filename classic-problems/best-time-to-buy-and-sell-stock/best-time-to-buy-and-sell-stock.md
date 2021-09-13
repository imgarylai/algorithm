# 121. Best Time to Buy and Sell Stock

[121. Best Time to Buy and Sell Stock](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/)

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

