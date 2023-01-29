# 677. Map Sum Pairs

[667. Map Sum Pairs](https://leetcode.com/problems/map-sum-pairs/)

```python
class TrieNode:
    def __init__(self, val = None):
        self.children = defaultdict(TrieNode)
        self.val = val

class MapSum:

    def __init__(self):
        """
        Initialize your data structure here.
        """
        self.root = TrieNode()


    def insert(self, key: str, val: int) -> None:
        node = self.root
        for char in key:
            node = node.children[char]
        node.val = val

    def sum(self, prefix: str) -> int:
        node = self.root
        for char in prefix:
            if char not in node.children.keys():
                return 0
            node = node.children[char]
        q = [[node]]
        res = 0
        while q:
            nodes = q.pop(0)
            tmp = []
            for node in nodes:
                if node.val:
                    res += node.val
                if node.children:
                    for key in node.children.keys():
                        tmp.append(node.children[key])
            if tmp:
                q.append(tmp)
        return res







# Your MapSum object will be instantiated and called as such:
# obj = MapSum()
# obj.insert(key,val)
# param_2 = obj.sum(prefix)
```

