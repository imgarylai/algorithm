# 425. Word Squares

[425. Word Squares](https://leetcode.com/problems/word-squares/)

```python
class Solution:
    def wordSquares(self, words: List[str]) -> List[List[str]]:

        square_width = len(words[0])
        trie = {}
        res = []
        for index, word in enumerate(words):
            node = trie
            for char in word:
                if char in node:
                    node = node[char]
                else:
                    node[char] = {
                        '#': []
                    }
                    node = node[char]
                node['#'].append(index)

        def backtrack(curr, step):
            if step == square_width:
                res.append(list(curr))
                return 
            else:
                prefix = ''.join([word[step] for word in curr])
                for word in getWordByPrefix(prefix):
                    curr.append(word)
                    backtrack(curr, step + 1)
                    curr.pop()

        def getWordByPrefix(prefix):
            node = trie
            for char in prefix:
                if char not in node:
                    return []
                node = node[char]
            return [words[index] for index in node['#']]

        for word in words:
            backtrack([word], 1)

        return res
```

