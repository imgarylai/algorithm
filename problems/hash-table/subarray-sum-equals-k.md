# 560. Subarray Sum Equals K

[560. Subarray Sum Equals K](https://leetcode.com/problems/subarray-sum-equals-k/)

給定一個陣列，要找一個子陣列的總和為 `K` 。

### 暴力法

我想到的方法是我先算出每個位置的 prefix sum ，之後我就看如果當前這個位置的 prefix sum 減掉前面某一個位置的 prefix sum ，如果說當好等於 `k` ，就代表這兩個位置之間的總和是 `k` ，也就是說前一個位置到當前這個位置的子陣列的總和是 `k` 。

有一個邊角情況要考慮，那就是第一個元素可能剛好就是 `k` ，所以我們的 `prefix_sum` 陣列前面要多放一個零的元素。這樣剛好第一個元素就是一個子陣列滿足總和是 `k` 。

先從 `[1..l]` 算出 prefix sum 。

接著從 `[i..l-1]` 開始，設定起始位置，然後看看從 `[i+1..l]` 是不是有兩個位置之間的差剛好是 `k` 。

```python
class Solution:
    def subarraySum(self, nums: List[int], k: int) -> int:
        
        count = 0
        l = len(nums)
        prefix_sum = [0] * (l+1)
        
        for i in range(1, l+1):
            prefix_sum[i] = prefix_sum[i - 1] + nums[i - 1]
        
        for i in range(l):
            for j in range(i+1, l+1):
                if prefix_sum[j] - prefix_sum[i] == k:
                    count += 1
                    
        return count
```

上面的方式，其實 `cumulative_sum` 在 外面的迴圈都是固定的。所以我們其實可以簡化成在外面的迴圈開始計算 `prefix_sum`。這個方法理論上跟前一個方法的時間複雜度是相同的，但是 Python 在 LeetCode 裡面會超時，不知道為什麼

```python
class Solution:
    def subarraySum(self, nums: List[int], k: int) -> int:
        
        count = 0
        l = len(nums)
        for i in range(l):
            prefix_sum = 0
            for j in range(i, l):
                prefix_sum += nums[j]
                if prefix_sum == k:
                    count += 1
        return count
```

### Hash Table 

這個方法比較特別一點，這個題目也是參考了兩個點

1. 如果剛好計算到該位置的時候，總和為 `k` ，那就子陣列總和為 k 的情況加一
2. 第二個情況和前面的情形有點像
   * 上面的視角是：「當前的位置減去前面某個位置的差值是不是 k？」
   * 這裡的視角是：「當前的位置減去 `k` 的差值，前面有沒有出現過？如果出現很多次，那就可以有組合出很多次的子陣列」例子：`[1, 2, 3, -7, 1, 2, 3, -7, 7]` 其中有兩個方法組合出 k 為 7 的子陣列
     * `[1, 2, 3, -7, 1, 2, 3, -7, 7]`
     * `[1, 2, 3, -7, 7]`   

所以使用 Hash Table 的方式，是我每次到該位置時，更新完所有的數字後，我要去記錄每個 prefix sum 的次數有出現幾次。

```python
class Solution:
    def subarraySum(self, nums: List[int], k: int) -> int:
               
        count = 0
        h = defaultdict(int)
        
        # 先計算每個 prefix_sum 的次數
        prefix_sum = 0
        for num in nums:
            prefix_sum += num
            h[prefix_sum] = h[prefix_sum] + 1
        
        # 1. 如果 prefix_sum 等於 k 計數加一
        # 2. 加上 prefix_sum - k 的計數，
        #    這裡不用 else 的情況是因為，如果前面有多次 prefix_sum 剛好是 0 
        #    那現在 prefix_sum 等於 k 的情況下，那些 prefix_sum 剛好是零的
        #    陣列都可以組成不同的 sub array 。
        prefix_sum = 0
        for num in nums:
            prefix_sum += num
            if prefix_sum == k:
                count += 1
            count += h[prefix_sum - k]
        return count
```

```python
class Solution:
    def subarraySum(self, nums: List[int], k: int) -> int:       
        count = 0
        h = defaultdict(int)
        cumulative_sum = 0
        
        for num in nums:
            cumulative_sum += num
            
            if cumulative_sum == k:
                count += 1
            
            count += h[cumulative_sum - k]
            h[cumulative_sum] = h[cumulative_sum] + 1
        
        return count
```



