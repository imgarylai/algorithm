# 309. Best Time to Buy and Sell Stock with Cool down

[309. Best Time to Buy and Sell Stock with Cool down](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-cooldown/)

```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        if len(prices) < 2:
            return 0
            
        buys = [float('-inf')] * len(prices)
        sells = [0] * len(prices)
        
        for i in range(len(prices)):
            buys[i] = max(buys[i-1] if i > 0 else -prices[i], (sells[i-2] if i > 1 else 0) - prices[i])
            sells[i] = max(sells[i-1] if i > 0 else 0, (buys[i-1] + prices[i] if i > 0 else 0))
        return sells[-1]
```

