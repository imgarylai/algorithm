# 122. Best Time to Buy and Sell Stock II

[122. Best Time to Buy and Sell Stock II](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii/)

```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        if len(prices) < 2:
            return 0

        buys = [float('-inf')] * len(prices) 
        sells = [0] * len(prices) 

        for i in range(len(prices)):
            if i == 0:
                buys[i] = max(buys[i], 0 - prices[i])
            else:
                buys[i] = max(buys[i-1], sells[i-1] - prices[i])
            sells[i] = max(sells[i-1], buys[i-1] + prices[i])
        return sells[-1]
```

