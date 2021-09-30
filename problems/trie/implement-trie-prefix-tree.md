# 208. Implement Trie \(Prefix Tree\)

[208. Implement Trie \(Prefix Tree\)](https://leetcode.com/problems/implement-trie-prefix-tree/)

```python
class TrieNode:
    # Initialize your data structure here.
    def __init__(self):
        self.children = defaultdict(TrieNode)
        self.is_word = False

class Trie:

    def __init__(self):
        """
        Initialize your data structure here.
        """
        self.root = TrieNode()


    def insert(self, word: str) -> None:
        """
        Inserts a word into the trie.
        """
        t = self.root
        for char in word:
            t = t.children[char]
        t.is_word = True


    def search(self, word: str) -> bool:
        """
        Returns if the word is in the trie.
        """
        t = self.root
        for char in word:
            if char not in t.children:
                return False
            t = t.children[char]
        return t.is_word


    def startsWith(self, prefix: str) -> bool:
        """
        Returns if there is any word in the trie that starts with the given prefix.
        """
        t = self.root
        for char in prefix:
            if char not in t.children:
                return False
            t = t.children[char]
        return True


# Your Trie object will be instantiated and called as such:
# obj = Trie()
# obj.insert(word)
# param_2 = obj.search(word)
# param_3 = obj.startsWith(prefix)
```

