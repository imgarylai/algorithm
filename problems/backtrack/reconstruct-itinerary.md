# 332. Reconstruct Itinerary

[332. Reconstruct Itinerary](https://leetcode.com/problems/reconstruct-itinerary/)

```python
class Solution:
    def findItinerary(self, tickets: List[List[str]]) -> List[str]:
        table = defaultdict(list)
        visited = defaultdict(list)
        for ticket in tickets:
            src = ticket[0]
            dst = ticket[1]
            table[src].append(dst)
        for key, item in table.items():
            item.sort()
            visited[key] = [False]*len(item)
        
        numTickets = len(tickets) + 1
        
        res = []
        def backtrack(src, curr):
            if len(curr) == numTickets:
                res.append(list(curr))
                return True
            for idx, dst in enumerate(table[src]):
                if not visited[src][idx]:
                    visited[src][idx] = True
                    ret = backtrack(dst, curr + [dst])
                    visited[src][idx] = False
                    if ret:
                        return True
                
        backtrack('JFK', ['JFK'])
        return res[0]
```

### 其他資源

我覺得講解最好的影片

{% embed url="https://www.youtube.com/watch?v=WYqsg5dziaQ" %}





