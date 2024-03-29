# 1167. Minimum Cost to Connect Sticks

[1167. Minimum Cost to Connect Sticks](https://leetcode.com/problems/minimum-cost-to-connect-sticks/)

這個題目的要求是說，每次要兩兩地把兩個木棍黏在一起，目標是要把所有的木棍黏在一起，不過每次黏的時候，木棍的長度會是他的成本，要求最小成本。

根據題目的敘述，我們可以推斷出每次黏和任兩根，卻要要求成本最短，那一定是要先把短的黏合成長的，因為如果先黏合長的，長的成本將會一直保留在後續的黏合行為裡。

基於上面的邏輯，我們也知道會有不斷的排序的情況，例如兩個短的可能一粘合後面的很長，就要先選擇其他較短的木棍來黏合，所以我們可以知道一定不是要靠先排序好來解決問題，要在挑選最大最小值，最快的情況就是使用 heap 來快速的查找。

每次先選出兩根組合後，再把組合好的木棍放回 heap 裡面，直到只剩下一根木頭為止。

時間複雜度為 $$O(nlogn)$$。 

```python
import heapq
class Solution:
    def connectSticks(self, sticks: List[int]) -> int:
        heap = []
        heapq.heapify(heap)
        for stick in sticks:
            heapq.heappush(heap, stick)
        ans = 0
        while len(heap) > 1:
            cost1 = heapq.heappop(heap)
            cost2 = heapq.heappop(heap)
            
            cost = cost1 + cost2
            ans += cost
            heapq.heappush(heap, cost)
            
        return ans
```

