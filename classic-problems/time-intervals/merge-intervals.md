# 56. Merge Intervals

[56. Merge Intervals](https://leetcode.com/problems/merge-intervals/)

這題只要解過了 [252. Meeting Rooms](meeting-rooms.md) 、 [253. Meeting Rooms II](meeting-rooms-ii.md) 就會非常的簡單。

[252. Meeting Rooms](meeting-rooms.md) 有教過了我們如何判斷區間重疊，這一個題目是我們要如何把重疊的區間都合併起來，並且給出所有的新時間區間。

這個題目還算好想一點，既然我們知道結果是一個陣列，那我們一開始就把第一個時間區間放到儲存結果的陣列，假設就只有一個時間區間，這就會是答案了。

接下來，我們就從後面的每一個時間區間來判斷，要如何得知前一個開會的時間呢？就是結果陣列的最後一個時間區間，接下來判斷是否需要合併，這個題目和前面兩個題目相比，比較特別的地方是，如果前一個時間區間的結束時間和後一個時間區間的開始區間相同時，我們是要合併的。

基本上就只有兩種情況，需要合併和不需要合併

先看如果說兩個時間不需要合併，這個比較簡單，我們就把當下的時間區間繼續放入就好。

如果說需要合併呢？這時候我們就需要重新計算新的時間區間，我們先把前一個時間區間拿出來，而新的時間區間很好計算，計算好再重新放入結果的陣列裡面。

```text
新的時間區間 = [兩個時間區間比較早的開始時間, 兩個時間區間比較晚的結束時間]
```

```python
class Solution:
    def merge(self, intervals: List[List[int]]) -> List[List[int]]:
        intervals.sort()
        stack = [intervals[0]]

        for i in range(1, len(intervals)):
            prevInterval = stack.pop()
            newInterval = intervals[i]
            if prevInterval[1] >= newInterval[0]:
                newInterval = [min(prevInterval[0], newInterval[0]), max(prevInterval[1], newInterval[1])]
            else:
                stack.append(prevInterval)
            stack.append(newInterval)
        return stack
```

