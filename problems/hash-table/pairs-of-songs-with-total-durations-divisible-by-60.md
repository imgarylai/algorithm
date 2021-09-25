# 1010. Pairs of Songs With Total Durations Divisible by 60

[1010. Pairs of Songs With Total Durations Divisible by 60](https://leetcode.com/problems/pairs-of-songs-with-total-durations-divisible-by-60/)



```python
class Solution:
    def numPairsDivisibleBy60(self, time: List[int]) -> int:
        table = defaultdict(int)
        ans = 0
        for t in time: 
            target = (60 - t % 60) % 60
            ans += table[target]
            table[t % 60] += 1
        return ans
```

