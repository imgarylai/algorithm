# 向矩陣中的四個方向移動

```python
row = 0
col = 0
directions = [(0, 1), (1, 0), (0, -1), (-1, 0)]
for drow, dcol in directions:
    if 0 <= row + drow < rows and 0 <= col + dcol < cols:
        # Do Something
```

{% page-ref page="../../classic-problems/robot-bounded-in-circle.md" %}

