# 陣列複製

在 LeetCode 裡面，很常遇到題目會需要將原先給定的陣列先儲存起來，例如：在對陣列操作的時候，需要一個原先的拷貝，之後需要跟原本的這個陣列做比較，這個技巧其實也滿常應用在現實生活的應用程式，在很多程式語言其實都會需要用到，所以我覺得大家一定都不陌生，真正麻煩的是觀念很好懂，但是在 LeetCode 寫題目的時候，題目一大，常常有一個小地方需要做一個淺拷貝的時候忘了，就很容易突然卡住沒 Debug 出來。

Python 陣列一共有三種拷貝

1. 賦值（Assignment）
2. 淺拷貝/複製（Shallow Copy）
3. 深拷貝/複製（Deep Copy）

## 賦值（Assignment）

```python
a = [1, 2, 3]
b = a
print(id(a), id(b), sep='\n')
# 4335753224
# 4335753224
```

`a` 和 `b` 都是在指同一個物件。

## 淺拷貝/複製（Shallow Copy）

```python
a = [1, 2, 3]
b = list(a)
print(id(a), id(b), sep='\n')
# 4335753224
# 4335754120
```

淺拷貝會建立一個新的物件，可以看到，兩個物件的 `id` 已經都不一樣了。但是如果看陣列裡面的子物件的話，他們所指向的對象還是一樣的。

```python
for i, j in zip(a,b):
    print(id(i), id(j))
# 4332150640 4332150640
# 4332150672 4332150672
# 4332150704 4332150704
```

## 深拷貝/複製（Deep Copy）

Python 的深拷貝就需要用到 `copy` 裡面的 `deepcopy` 但是如果用之前的方法來檢查，會發現結果怎麼還是會一樣？

```python
import copy
b = copy.deepcopy(a)
for i, j in zip(a, b):
    print(id(i), id(j))
# 4332150640 4332150640
# 4332150672 4332150672
# 4332150704 4332150704
```

真正的原因是因為：[https://en.wikipedia.org/wiki/String\_interning](https://en.wikipedia.org/wiki/String_interning)

這時候用另外一個例子來看

```text
import copy
a = [[1, 2, 3],[4, 5, 6]]
b = list(a)
c = copy.deepcopy(a)
print(id(a), id(b), id(c), sep=`\n`)
# 4335753352
# 4335775880
# 4335753608
# => 三個物件的 id 都不相同
for i, j in zip(a, b):
    print(id(i), id(j))
# 4335754120 4335754120
# 4335753928 4335753928
# => a, b 的字物件 id 都相同
for i, j in zip(a, c):
    print(id(i), id(j))
# 4335754120 4335753224
# 4335753928 4335755144
# => a, c 的子物件 id 不相同
```

