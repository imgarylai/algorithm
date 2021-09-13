# 22. Generate Parentheses

[22. Generate Parentheses](https://leetcode.com/problems/generate-parentheses/)

這一題和 [46. Permutations](permutations/) 很類似，題目要求的就是要窮舉。  

```python
class Solution:
    def generateParenthesis(self, n: int) -> List[str]:
        ans = []
        def backtrack(curr = [], left = 0, right = 0):
            if left == n and right == n:
                ans.append(''.join(curr))
                return
            if left < n:
                curr.append('(')
                backtrack(curr, left + 1, right)
                curr.pop()
            if right < left:
                curr.append(')')
                backtrack(curr, left, right + 1)
                curr.pop()
                
        backtrack()
        return ans
```

