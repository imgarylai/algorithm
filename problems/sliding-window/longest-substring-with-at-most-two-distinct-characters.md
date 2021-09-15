# 159. Longest Substring with At Most Two Distinct Characters

[159. Longest Substring with At Most Two Distinct Characters](https://leetcode.com/problems/longest-substring-with-at-most-two-distinct-characters/)

```python
class Solution:
    def lengthOfLongestSubstringTwoDistinct(self, s: str) -> int:
        fast = 0
        slow = 0
        memo = defaultdict(int)
        res = 0
        while fast < len(s):
            char = s[fast]
            fast += 1
            
            memo[char] += 1
            
            while len(memo) > 2:
                d = s[slow]
                slow += 1
                memo[d] -= 1
                if memo[d] == 0:
                    del memo[d]
            res = max(res, fast - slow)
        return res
```

