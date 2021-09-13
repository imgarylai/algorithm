# 1170. Compare Strings by Frequency of the Smallest Character

[1170. Compare Strings by Frequency of the Smallest Character](https://leetcode.com/problems/compare-strings-by-frequency-of-the-smallest-character/)

```python
class Solution:
    def f(self, word):
        lexicalOrder = sorted(word)
        counter = collections.Counter(lexicalOrder)
        return counter[lexicalOrder[0]]
    def numSmallerByFrequency(self, queries: List[str], words: List[str]) -> List[int]:
        queryFreqs = [self.f(query) for query in queries]
        wordFreqs = [self.f(word) for word in words]
        ans = []
        for queryFreq in queryFreqs:
            count = 0
            for wordFreq in wordFreqs:    
                if wordFreq > queryFreq:
                    count += 1
            ans.append(count)
        return ans
```



