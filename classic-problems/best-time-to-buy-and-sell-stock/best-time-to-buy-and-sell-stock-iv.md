# 188. Best Time to Buy and Sell Stock IV

[188. Best Time to Buy and Sell Stock IV](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iv)

```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        firstBuy, firstSell = float('-inf'), 0
        secondBuy, secondSell = float('-inf'), 0

        for price in prices:
            firstBuy = max(firstBuy, -price)
            firstSell = max(firstSell, firstBuy + price)
            secondBuy = max(secondBuy, firstSell - price)
            secondSell = max(secondSell, secondBuy + price)

        return secondSell
```

