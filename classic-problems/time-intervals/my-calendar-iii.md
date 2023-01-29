# 732. My Calendar III

[732. My Calendar III](https://leetcode.com/problems/my-calendar-iii/)

題目在考 [253. Meeting Rooms II](meeting-rooms-ii.md) 。

```python
class MyCalendarThree:

    def __init__(self):
        self.intervals = []

    def minMeetingRooms(self, intervals: List[List[int]]) -> int:
        intervals.sort()

        heap = []

        heapq.heappush(heap, intervals[0][1])    
        count = 1

        for i in range(1, len(intervals)):

            interval = intervals[i]


            if interval[0] >= heap[0]:
                heapq.heappop(heap)  
            else:
                count += 1

            heapq.heappush(heap, interval[1])
        return count


    def book(self, start: int, end: int) -> int:
        self.intervals.append((start, end))
        return self.minMeetingRooms(self.intervals)


# Your MyCalendarThree object will be instantiated and called as such:
# obj = MyCalendarThree()
# param_1 = obj.book(start,end)
```

