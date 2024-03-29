# 84. Largest Rectangle in Histogram

[84. Largest Rectangle in Histogram](https://leetcode.com/problems/largest-rectangle-in-histogram/)

我一開始想的想法是雙指針的做法，那就是我一樣從左右往中間逼近，但是呢，逼近的過程中我先找出哪個高度最低，那這個高度就會決定了在目前左右寬的情況下，最大的面積，但是這樣並不能保證一定是最大的面積，可是我們已經把最短的邊給使用掉了，接下來我就從當下的座標，往左往右尋找，在剔除最短的高度的情況下，縮短寬度是不是有機會有更大的高度來算出更大的矩形。

## 遞迴法：（超時？）

```python
class Solution:
    def largestRectangleArea(self, heights: List[int]) -> int:       
        def helper(start, end):
            if start > end:
                return 0
            min_h_index = start
            # searching space from start to end + 1
            for i in range(start, end + 1):
                if heights[i] < heights[min_h_index]:
                    min_h_index = i
            return max(heights[min_h_index] * (end - start + 1 ), helper(start, min_h_index - 1), helper(min_h_index + 1, end))
        return helper(0, len(heights) - 1)
```

我個人會覺得，如果在面試可以寫出以上的寫法，並不算太差，不過這題不存在著重疊子問題，所以也沒辦法用 DP 來優化。

```python
class Solution:
    def largestRectangleArea(self, heights: List[int]) -> int:
        n = len(heights)
        if n == 0:
            return 0
        if len == 1:
            return heights[0]
        area = 0
        
        stack = []
        for i in range(n):
            while stack and heights[stack[-1]] > heights[i]:
                height = heights[stack.pop()]
                while stack and heights[stack[-1]]  == height:
                    stack.pop()
                
                width = 0
                if not stack:
                    width = i
                else:
                    width = i - stack[-1] - 1
                
                area = max(area, width * height)
            stack.append(i)
            
        while stack:
            height = heights[stack.pop()]
            
            while stack and heights[stack[-1]]  == height:
                    stack.pop()
            width = 0
            if not stack:
                width = n
            else:
                width = n - stack[-1] - 1
                
            area = max(area, width * height)
            
        return area
            
        
        
        # stack = [-1]
        # heights.append(0)
        # ans = 0
        # for i, height in enumerate(heights):
        #     while heights[stack[-1]] > height:
        #         h = heights[stack.pop()] 
        #         w = i - stack[-1] - 1
        #         ans = max(ans, h*w)
        #     stack.append(i)
        # return ans
        
        # max_area = 0
        # for i in range(len(heights)):
        #     min_height = float('inf')
        #     for j in range(i, len(heights)):
        #         min_height = min(min_height, heights[j])
        #         max_area = max(max_area, min_height * (j - i + 1))
        # return max_area
        
#         def helper(start, end):
#             if start > end:
#                 return 0
#             min_index = start
#             for i in range(start, end + 1):
#                 if heights[min_index] > heights[i]:
#                     min_index = i
#             return max(
#                 heights[min_index] * (end - start + 1),
#                 helper(start, min_index - 1),
#                 helper(min_index + 1, end),
#             )
            
#         return helper(0, len(heights) - 1)
        
        
        
```

