# 188. Best Time to Buy and Sell Stock IV

[188. Best Time to Buy and Sell Stock IV](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iv)

```python
class Solution:
    def maxProfit(self, k: int, prices: List[int]) -> int:
        if len(prices) < 2 or k < 1:
            return 0
        
        if k > len(prices)//2:
            max_profit = 0
            for i in range(1, len(prices)):
                max_profit += max(0, prices[i] - prices[i-1])
            return max_profit
            
        buys = [float('-inf')] * k
        sells = [0] * k
        
        for price in prices:
            for i in range(k):
                if i == 0:
                    buys[i] = max(buys[i], 0 - price)
                else:
                    buys[i] = max(buys[i], sells[i-1] - price)
                sells[i] = max(sells[i], buys[i] + price)
        return sells[-1]
```

