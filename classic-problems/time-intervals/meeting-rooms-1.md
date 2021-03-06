# 252. Meeting Rooms

[252. Meeting Room](https://leetcode.com/problems/meeting-rooms/)

這個題目是所有題目的基礎，題目給定一連串的時間序列，且時間序列是**亂序的**，想問這些時間區間有沒有重複？

雖然說題目是簡單，我覺得這只是題目的解法很簡單，但是如果第一次看到題目，到底要從哪裡開始想，我覺得還是有挑戰性的。

面試遇到不會的題目，就是先冷靜觀察，先看看如果我們只有兩個區間，我們要如何判斷時間有重疊？

* \[1, 6\] 和 \[2, 5\]：前面的區間誇度大，區間大到包含了後面的所有時間區間。
* \[1, 4\] 和 \[2, 5\]：前一個的區間，剛好跨過了後一個區間的開始時間。
* \[3, 6\] 和 \[2, 5\]：前一個的區間，剛好從後面區間的中間開始。
* \[3, 4\] 和 \[2, 5\]：前一個區間跨度小，區間剛好被後面的所有區間包含。
* \[1, 3\] 和\[3,6\]：前一個區間的時間結束時間與後一個時間區間的開始時間相同，**不算是重疊**。

我當時觀察到這裡，其實開始想了一下自己的解法對不對，一次比兩個區間很簡單，但是整個數列的區間都是亂排的，我要怎麼樣都全部比完呢？是不是有什麼地方我沒有想到？

{% hint style="warning" %}
我覺得在面試的時候最怕的就是這種情況，我們按照題目的敘述開始展開思路，但是到底我們的思路對不對？其實在真的寫完之前，都不知道，不過其實真正面試時遇到的題目，很少很少會出現需要「跳脫思考」的題目，如果有公司真的喜歡出這種題目，就算是夢想公司我也會希望當下不要覺得要太難過，因為30~45分中就要想出跳脫思考，這表示這間公司的選人來說是的標準是不可觀的。真的遇到這樣的情況，反而應該要先問問面試官，我想的方向對不對就好？
{% endhint %}

這個題目的難度不高，其實不會到想不到解法啦，上面的話只是給自己信心，要相信自己可以在面試中表現好，回到題目繼續觀察，其實第三、第四點，如果我們把前後的區間對調，滿足他們重疊的情況，就會變成一模一樣了，我在第一次寫題目的當下就覺得是人腦在思考時有時候太快，反而讓我自己產生了盲點。

於是這類型題目最重要的一個轉折點就出現了，那就是**如果我們可以把所有的時間區間，先不用管結束時間，而是以按照開始的時間為基準，由小到大排列**，那我們就可以用另外一個條件來判斷時間是否重疊，那就是：

{% hint style="info" %}
前一個時間區間的結束時間，不能大於後一個時間區間的開始時間
{% endhint %}

題目其實就簡化成了另一個問題，如何將題目的時間區間按照開始時間由小到大排列。這邊最後的題目我使用了 python 預設的 sort\(\) 語法來做到，不過在面試的時候，可能會不知道原來 python 的 sort\(\) 可以滿足這樣的需求，但是這也沒有問題，因為 heap 的用法就是面試前一定要準備到的，也可以使用 heap 來重新去做到排序。

因此只要時間排序好了，就可以用上面的判斷式直接去回答題目的問題了。

```python
class Solution:
    def canAttendMeetings(self, intervals: List[List[int]]) -> bool:
        if not intervals:
            return True
        intervals.sort()

        for i in range(1, len(intervals)):
            previous_begin_time, previous_end_time = intervals[i - 1]
            current_begin_time, current_end_time = intervals[i]
            if current_begin_time < previous_end_time:
                return False

        return True
```

