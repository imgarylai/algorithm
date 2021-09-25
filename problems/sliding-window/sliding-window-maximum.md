# 239. Sliding Window Maximum

[239. Sliding Window Maximum](https://leetcode.com/problems/sliding-window-maximum/)

這一題是滑動窗口的問題，不過困難的點是在於如何收縮窗口，直接透過程式碼的註解解釋會比較容易。

這裡會用到的是 `queue` 來記錄「位置」一直紀錄 `i-k` 到 `i` 之間的資訊。

```python
class Solution:
    def maxSlidingWindow(self, nums: List[int], k: int) -> List[int]:
        n = len(nums)
        if n == 0 or k == 0: return []
        
        queue = deque()
        ans = []
        
        max_id = 0
        for i in range(k):
            # 如果最 queue 最左邊的值超過範圍了，要退出
            if queue and queue[0] == i - k:
                queue.popleft()
            # 如果當前比最後一個值大，那就不斷的把最後一個數字退出
            # 這樣可以確保最左邊的所記錄的位置，其位置的數字一定是最大的
            while queue and nums[i] > nums[queue[-1]]:
                queue.pop() 
            # 如果當時 queue 的每一個數字都比現在的數字小，就會全部退出完，
            # 現在放進去的就是最大的
            # 如果當時 queue 的最後一個位置的值，比起現在的數字大
            # 那就會保留在最左邊
            queue.append(i)
            
            # 更新最大值的 id 
            if nums[i] > nums[max_id]:
                max_id = i
        ans.append(nums[max_id])
        
        # 後面同理
        for i in range(k, n):
            if queue and queue[0] == i - k:
                queue.popleft()
            while queue and nums[i] > nums[queue[-1]]:
                queue.pop()
            queue.append(i)
            ans.append(nums[queue[0]])
        return ans
```

