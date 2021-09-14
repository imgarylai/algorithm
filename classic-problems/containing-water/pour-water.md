# 755. Pour Water

[755. Pour Water](https://leetcode.com/problems/pour-water/)

```python
class Solution:
    def pourWater(self, heights: List[int], volume: int, k: int) -> List[int]:
        for _ in range(volume):
            
            # start pouring left
            left = k
            for i in range(k - 1, -1, -1):
                # hit left wall, stop
                if heights[i] > heights[i + 1]:
                    break
                # droplet go to lower place
                elif heights[i] < heights[i + 1]:
                    left = i
                # droplet stay 
                else:
                    continue
            # if left != k mean droplet goes to left, stop this iteration
            if left != k:
                heights[left] += 1
                continue
            
            # otherwise, droplet start pouring right
            right = k
            for i in range(k + 1, len(heights)):
                # hit right, wall
                if heights[i] > heights[i - 1]:
                    break
                # droplet go to lower place
                elif heights[i] < heights[i - 1]:
                    right = i
                # droplet stay     
                else:
                    continue
            if right != k:
                heights[right] += 1
            else:
                heights[k] += 1
        return heights
            
                    
```

