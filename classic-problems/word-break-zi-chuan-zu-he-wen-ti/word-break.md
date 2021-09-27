# 139. Word Break

[139. Word Break](https://leetcode.com/problems/word-break/)

每次檢查一個單字，看看單字有沒有符合是目標字串的前綴字元，如果說有符合的話，繼續從剩的字串檢查下去，剩餘的字串起始位置是符合的單字的長度。

## 遞迴

```python
class Solution:
    def wordBreak(self, s: str, wordDict: List[str]) -> bool:
        wordDict = set(wordDict)
        def helper(s):
            if len(s) == 0:
                return True
            for word in wordDict:
                if len(word) <= len(s):
                    if s.startswith(word):
                        if helper(s[len(word):]):
                            return True
            return False
        return helper(s)
```

遞迴的方式有很多重複的子問題，例如目標字串是 `code` ，字典是：`[c, o, co, de]` ，`de` 就是重疊子問題，所以所以利用記憶法來避免重複的子問題。

## 自頂向下

```python
class Solution:
    def wordBreak(self, s: str, wordDict: List[str]) -> bool:
        wordDict = set(wordDict)
        memo = {}
        def helper(s):
            if len(s) == 0:
                return True
            if s in memo:
                return memo[s]
            for word in wordDict:
                if len(word) <= len(s):
                    if s.startswith(word):
                        if helper(s[len(word):]):
                            memo[s] = True
                            return memo[s]
            memo[s] = False
            return memo[s]
        return helper(s)
```

## 自底向上

做法有點不直覺，處理的邏輯是一步一步走，去檢查每一個位置，有沒有機會可以用任何字典中的單字拼起來。檢查的邏輯如下：

例如：我站在某位置 `j` ，接著我就從位置 `i = 0` 一路檢查到位置 `j` ，看看有沒有辦法在位置 `i` 的地方其中 `s[i:j]` 剛好在字典裡面，但是這樣還不夠，那就是在位置 `i` 的地方，也要有字串可以到達才夠，如果兩個條件都滿足，那 `dp[j]` 就會是 True ，代表可以到達這個地方。

```python
class Solution:
    def wordBreak(self, s: str, wordDict: List[str]) -> bool:

        dp = [False] * (len(s) + 1)
        dp[0] = True

        for end in range(1, len(s)+1):
            for start in range(end):
                if dp[start] and s[start:end] in wordDict:
                    dp[end] = True
                    break

        return dp[len(s)]
```

## 回溯法

這一題其實也可以用回溯法來寫，道理很類似，回溯法也是遞迴的一種，只要加上記憶法就可以了。

這樣的寫法值得參考是因為這個題目的變形，困難難度的題目，就可以用回溯法來寫。

```python
class Solution:
    def wordBreak(self, s: str, wordDict: List[str]) -> bool:

        wordDictSet = set(wordDict)

        memo = {}
        ans = []
        def helper(s, curr):
            if len(s) == 0:
                ans.append(' '.join(curr))
                return True
            if s in memo:
                return memo[s]
            else:
                for word in wordDictSet:
                    if len(word) <= len(s):
                        if s.startswith(word):
                            curr.append(word)
                            if helper(s[len(word):], curr):
                                memo[s[len(word):]] = True
                                return memo[s[len(word):]]
                            curr.pop()
                memo[s] = False
                return memo[s]

        return helper(s, [])
```

