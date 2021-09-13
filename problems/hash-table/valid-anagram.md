# 242. Valid Anagram

[242. Valid Anagram](https://leetcode.com/problems/valid-anagram/)

```python
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        table = defaultdict(int)
        for char in s:
            table[char] += 1

        for char in t:
            if table[char] > 0:
                table[char] -= 1
            else:
                return False

        for key in table.keys():
            if table[key] != 0:
                return False

        return True
```

