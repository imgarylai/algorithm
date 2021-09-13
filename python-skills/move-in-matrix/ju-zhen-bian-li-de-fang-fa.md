# 矩陣遍歷的方法

## TODO

### 初階

#### 從左到右，從上到下

```python
step = 1
for row in range(n):
    for col in range(n):
        matrix[row][col] = step
        step += 1
print_matrix(matrix)

# 1  2  3  4  5  
# 6  7  8  9  10 
# 11 12 13 14 15 
# 16 17 18 19 20 
# 21 22 23 24 25
```

#### 從上到下，從左到右

```python
step = 1
for row in range(n):
    for col in range(n):
        matrix[col][row] = step
        step += 1
print_matrix(matrix)

# 1  6  11 16 21 
# 2  7  12 17 22 
# 3  8  13 18 23 
# 4  9  14 19 24 
# 5  10 15 20 25
```

#### 從右到左，從上到下

`col` 要從最後一個開始取

```python
step = 1
for row in range(n):
    for col in range(n):
        matrix[row][n - col - 1] = step
        step += 1
print_matrix(matrix)

# 5  4  3  2  1  
# 10 9  8  7  6  
# 15 14 13 12 11 
# 20 19 18 17 16 
# 25 24 23 22 21
```

#### 從上到下，從右到左

col 會先遍歷，所以先走 col （當成 row），row 比較後面遍歷，當作 col ，又因為需要從右到左，所以從尾部開始遍歷。

```python
step = 1
for row in range(n):
    for col in range(n):
        matrix[col][n - row - 1] = step
        step += 1
print_matrix(matrix)

# 21 16 11 6  1  
# 22 17 12 7  2  
# 23 18 13 8  3  
# 24 19 14 9  4  
# 25 20 15 10 5
```

#### 從左到右，從下往上

```python
step = 1
for row in range(n):
    for col in range(n):
        matrix[n-row-1][col] = step
        step += 1
print_matrix(matrix)

# 21 22 23 24 25 
# 16 17 18 19 20 
# 11 12 13 14 15 
# 6  7  8  9  10 
# 1  2  3  4  5
```

#### 從下往上，從左到右

```python
step = 1
for row in range(n):
    for col in range(n):
        matrix[n-col-1][row] = step
        step += 1
print_matrix(matrix)

# 5  10 15 20 25 
# 4  9  14 19 24 
# 3  8  13 18 23 
# 2  7  12 17 22 
# 1  6  11 16 21
```

#### 從右到左，從下往上

```python
step = 1
for row in range(n):
    for col in range(n):
        matrix[n-row-1][n-col-1] = step
        step += 1
print_matrix(matrix)

# 25 24 23 22 21 
# 20 19 18 17 16 
# 15 14 13 12 11 
# 10 9  8  7  6  
# 5  4  3  2  1
```

#### 從下往上，從右到左

```python
step = 1
for row in range(n):
    for col in range(n):
        matrix[n-col-1][n-row-1] = step
        step += 1
print_matrix(matrix)

# 25 20 15 10 5  
# 24 19 14 9  4  
# 23 18 13 8  3  
# 22 17 12 7  2  
# 21 16 11 6  1
```

### 進階

#### 從左上到右下，上半部，包含對角線

* 第一次走對角線，總共會遍歷 n \(-0\) 個數量的 row，col 向右平移 0 個單位
* 第二次走對角線，總共會遍歷 n - 1個數量的 row ，col 向右平移 1 個單位
* 第 n - 1 次走對角線，總共會遍歷 n - \(n - 1\) 個數量的 row ，col 向右平移 \(n - 1\) 個單位

```python
step = 1
# [0..n-1]
for length in range(n):
    for row in range(n - length):
        col = row + length
        matrix[row][col] = step
        step += 1
print_matrix(matrix)

# 1  6  10 13 15 
# 0  2  7  11 14 
# 0  0  3  8  12 
# 0  0  0  4  9  
# 0  0  0  0  5
```

#### 從左上到右下，下半部

```python
step = 1
for length in range(n):
    for row in range(n - length):
        col = row + length
        matrix[col][row] = step
        step += 1
print_matrix(matrix)

# 1  0  0  0  0  
# 6  2  0  0  0  
# 10 7  3  0  0  
# 13 11 8  4  0  
# 15 14 12 9  5
```

#### 從右下到左下，上半部

```python
step = 1
for length in range(n):
    for row in range(n - length):
        col = row + length
        matrix[n-col-1][n-row-1] = step
        step += 1
print_matrix(matrix)

# 5  9  12 14 15 
# 0  4  8  11 13 
# 0  0  3  7  10 
# 0  0  0  2  6  
# 0  0  0  0  1
```

#### 從右下到左下，下半部

```python
step = 1
for length in range(n):
    for row in range(n - length):
        col = row + length
        matrix[n-row-1][n-col-1] = step
        step += 1
print_matrix(matrix)

# 5  0  0  0  0  
# 9  4  0  0  0  
# 12 8  3  0  0  
# 14 11 7  2  0  
# 15 13 10 6  1
```

