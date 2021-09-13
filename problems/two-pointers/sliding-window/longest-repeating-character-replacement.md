# 424. Longest Repeating Character Replacement

[424. Longest Repeating Character Replacement](https://leetcode.com/problems/longest-repeating-character-replacement/)

```python
class Solution:
    def characterReplacement(self, s: str, k: int) -> int:
        slow = 0
        fast = 0
        table = defaultdict(int)
        max_count = 0
        res = 0
        while fast < len(s):
            char = s[fast]
            table[char] += 1
            fast += 1
            max_count = max(max_count, table[char])
            if (fast - slow) > (max_count + k):
                char = s[slow]
                table[char] -= 1
                slow += 1
            res = max(res, fast - slow)
        return res
```

