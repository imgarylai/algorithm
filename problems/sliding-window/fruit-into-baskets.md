# 904. Fruit Into Baskets

[904. Fruit Into Baskets](https://leetcode.com/problems/fruit-into-baskets/)

```python
class Solution:
    def totalFruit(self, fruits: List[int]) -> int:
        fast = 0
        slow = 0
        ans = 0
        memo = defaultdict(int)
        while fast < len(fruits):
            fruit = fruits[fast]
            fast += 1
            memo[fruit] += 1

            while len(memo) > 2:
                d = fruits[slow]
                slow += 1
                memo[d] -= 1
                if memo[d] == 0:
                    del memo[d]
            ans = max(fast - slow, ans)
        return ans
```

