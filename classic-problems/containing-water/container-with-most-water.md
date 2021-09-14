# 11. Container With Most Water

[11. Container With Most Water](https://leetcode.com/problems/container-with-most-water/)

題目給出的正是水桶高度，在本題組的前言有提到水桶的最大容量怎麼算，當時的假設是底面積固定，這個題目裡面，給定的數字是我們有著水桶的兩個邊，其兩個邊之間的距離就是水桶的底面積，因次我們會有不同的水桶面積與水桶壁的高度組合。

所以題目要求的就是所有的排列組合中，哪個水桶容量最大，可以裝最多水。

### 窮舉

```python
class Solution:
    def maxArea(self, height: List[int]) -> int:
        area = float('-inf')
        
        for end in range(1, len(height)):
            for start in range(end):
                width = end - start
                area = max(area, min(height[start], height[end]) * width)
                
        return area
```

時間複雜度為 $$O(n^{2})$$ 。

### 雙指針

這個題目有另外一個解法，是使用雙指針的方法來加速決定的過程。

窮舉法的缺點就在於它是無差別的去比較所有的東西，這個題目其實有兩個很明顯的定義是有辦法讓我們加速查找到結果的。

1. 水桶的水量會被短邊決定
2. 底面積越大，又有更大的邊時，可以裝更多的水，高度也不一定是要最高的，反之，如果底面積太小，即使水桶邊很高，也可能導致水量不夠多。

水桶的高度是需要遍歷一次才能知道，不過我們可以很快地知道**最大**的底面積是多少，那就是題目給定的陣列的長度。

接下來我們可以查找的底面積，就是從這個最大底面積往最小底面積開始找，這樣就可以變成一個線性的查找，時間複雜度可以到 $$O(n)$$ ，當然我們還要看搜索的過程中有沒有其他的操作有影響時間複雜度。

雖然我們要一路從最大底面積往最小底面積搜索，不過我們並不是直接從最右邊往最左邊搜尋，因為如果是這樣的話，水桶的一邊就被固定住了，所以我們應該要從水桶的兩邊往中間逼近。

因此下一步是要決定的是，我們要從左邊往中間逼近，還是從右邊往中間逼近？回到裝水問題的核心，當底面積固定的時候，水桶的最大容量是由較短邊的高度決定，因此查找的過程就可以寫出來了。

這裡要注意的就是，我們要怎麼判斷搜尋的邊界？是 `left < right` 還是 `left <= right` ？寬度是 `right - left` 還是 `right - left + 1` ，以及他們的意義分別是什麼？

中間的查找過程中，只有比較和運算，因此不會影響時間複雜度，這個題目的時間複雜度為 $$O(n) $$ 。

```python
class Solution:
    def maxArea(self, height: List[int]) -> int:
        left = 0
        right = len(height) - 1
        area = float('-inf')
        
        while left < right:
            leftHeight = height[left]
            rightHeight = height[right]
            width = right - left
            area = max(area, min(leftHeight, rightHeight) * width)
            if leftHeight > rightHeight:
                right -= 1
            else:
                left += 1
                
        return area
```

