# 731. My Calendar II

[731. My Calendar II](https://leetcode.com/problems/my-calendar-ii/)

同 [729. My Calendar I](my-calendar-i.md) 的題目，不過需要多記錄一個重疊的問題。

```python
class MyCalendarTwo:
    def __init__(self):
        self.calendar = []
        self.overlaps = []

    def book(self, start, end):
        for i, j in self.overlaps:
            if start < j and end > i:
                return False
        for i, j in self.calendar:
            if start < j and end > i:
                self.overlaps.append((max(start, i), min(end, j)))
        self.calendar.append((start, end))
        return True



# Your MyCalendarTwo object will be instantiated and called as such:
# obj = MyCalendarTwo()
# param_1 = obj.book(start,end)
```

