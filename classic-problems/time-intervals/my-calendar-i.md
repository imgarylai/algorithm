# 729. My Calendar I

[729. My Calendar I](https://leetcode.com/problems/my-calendar-i/)

插入時間的結束時間比當前時間的開始時間小，且插入時間的開始時間比當前的結束時間小 -&gt; 發生重疊。

```python
class MyCalendar(object):
    def __init__(self):
        self.calendar = []

    def book(self, start, end):
        for s, e in self.calendar:
            if s < end and start < e:
                return False
        self.calendar.append((start, end))
        return True


# Your MyCalendar object will be instantiated and called as such:
# obj = MyCalendar()
# param_1 = obj.book(start,end)
```

