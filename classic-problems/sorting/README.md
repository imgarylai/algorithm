# Custom sorting 排序技巧

排序有分兩種

1. `sorted()` ：回傳排序好的陣列，原陣列不改變
2. `arr.sort()` ：直接針對原陣列排序好，原陣列的順序會不存在

兩者的 API 都差不多

## 陣列

### 升冪排序

```python
a = [1, 3, 2, 5, 4]
a.sort()
# [1, 2, 3, 4, 5]
```

### 降冪排序

第一種方法，使用 reverse

```python
a = [1, 3, 2, 5, 4]
a.sort(reverse=True)
# [5, 4, 3, 2, 1]
```

第二種方法，使用 Key

```python
a = [1, 3, 2, 5, 4]
a.sort(key=lambda x: (-x))
# [5, 4, 3, 2, 1]
```

### 二維陣列排序（降冪排序同一維陣列）

```python
a = [[2, 3], [1, 4], [1, 2], [1, 5], [4, 6]]
a.sort()
# [[1, 2], [1, 4], [1, 5], [2, 3], [4, 6]]
```

### 二維陣列按照第一個元素升冪排列，第二的元素降冪排列

```python
a = [[2, 3], [1, 4], [1, 2], [1, 5], [4, 6]]
a.sort(key=lambda x: (x[0],-x[1]))
# [[1, 5], [1, 4], [1, 2], [2, 3], [4, 6]]
```

這種排序方法常用在跟區間相關的題目：

{% page-ref page="../longest-increasing-subsequence/russian-doll-envelopes.md" %}

{% page-ref page="../time-intervals/video-stitching.md" %}

### 按照字典序（lexicographic order）排序

```python
words = ['apple', 'apple', 'orange', 'banana']
words.sort()
```

## Dict

### 按照 key 排序

```python
table = {1: 1, 3: 3, 4: 4, 2: 2}
for key in sorted(table.keys()):
    print(table[key])
```

按照 value 排序

```python
table = {1: 1, 3: 3, 4: 4, 2: 2}
for key, val in sorted(table.items(), key=lambda kv: (kv[1], kv[0])):
    print('table[{}] = {}'.format(key, val))
```

