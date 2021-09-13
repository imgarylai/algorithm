# 386. Lexicographical Numbers

[386. Lexicographical Numbers](https://leetcode.com/problems/lexicographical-numbers/)

```python
class Solution:
    def lexicalOrder(self, n: int) -> List[int]:
        strArr = [str(i) for i in range(1,n+1)]
        strArr.sort()
        return [int(s) for s in strArr]
```

### 參考

{% page-ref page="../../python-skills/sorting.md" %}

