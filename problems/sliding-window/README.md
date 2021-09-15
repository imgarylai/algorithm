# Sliding Window 滑動窗口

滑動窗口題目算是雙指針的一類題目，不過不同於其他雙指針是從兩邊出發，滑動窗口的題目是同向出發。

在處理滑動窗口的問題的時候，我們需要注意以下四個問題

1. 我們需要想的是窗口增大的時候，需要更新哪些資訊？
2. 何時要收縮窗口？
3. 收縮窗口時，需要更新哪些資訊？
4. 最終結果要在「擴大窗口」時更新還是「收縮窗口」時更新？

```python
left = 0
right = 0
table = defaultdict(int)
while (right < len(arr)):
    # Do something
    table[arr[right]] += 1
    right += 1

    while (table[arr[right]] > 1):
        # Do something
        table[arr[left]] -= 1
        left += 1
```

