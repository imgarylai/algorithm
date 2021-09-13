# 140. Word Break II

[140. Word Break II](https://leetcode.com/problems/word-break-ii/)

這一題可以參考 [139. Word Break](../dynamic-programming/word-break.md#hui-su-fa) 。 

```python
class Solution:
    def wordBreak(self, s: str, wordDict: List[str]) -> List[str]:
        
        
        wordDictSet = set(wordDict)
        
        ans = []
        def helper(s, curr):
            if len(s) == 0:
                ans.append(' '.join(curr))
                return
            else:
                for word in wordDictSet:
                    if len(word) <= len(s):
                        if s.startswith(word):
                            curr.append(word)
                            helper(s[len(word):], curr)
                            curr.pop()
        
        helper(s, [])
        return ans
```

