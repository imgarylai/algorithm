# 271. Encode and Decode Strings

[271. Encode and Decode Strings](https://leetcode.com/problems/encode-and-decode-strings/)

```python
class Codec:
    def __init__(self, size = 3):
        self.size = size
    
    def encode(self, strs: [str]) -> str:
        """Encodes a list of strings to a single string.
        """
        res = ''
        
        for s in strs:
            chunk_size = len(s)
            meta = str(len(s)).zfill(self.size)
            res += meta + s
        
        return res
            
    
    def decode(self, s: str) -> [str]:
        """Decodes a single string to a list of strings.
        """
        res = []
        i = 0
        
        while i < len(s):
            meta = s[i:i+self.size]
            chunk_size = int(meta)
            i += self.size
            string = s[i:i+chunk_size]
            res.append(string)
            i += chunk_size
        
        return res
            
        


# Your Codec object will be instantiated and called as such:
# codec = Codec()
# codec.decode(codec.encode(strs))
```

