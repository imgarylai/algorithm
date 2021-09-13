# 279. Perfect Squares

[279. Perfect Squares](https://leetcode.com/problems/perfect-squares/)

```python
class Solution:
    def numSquares(self, n: int) -> int:
        
        children = [i * i for i in range(1, int(n**0.5)+1)]
        
        queue = deque([n])
        level = 0
        
        while queue:
            level += 1
            size = len(queue)
            for i in range(size):
                node = queue.popleft()
                for child in children:
                    if child == node:
                        return level
                    elif child > node:
                        break
                    else:
                        queue.append(node - child)
```

