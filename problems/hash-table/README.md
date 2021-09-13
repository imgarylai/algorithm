# Hash Table/Set

在 LeetCode 裡面，Hash Table 是一個很好用而且很常用的資料結構，**增、刪、查、改**的時間複雜度是 O\(1\)  。在 Python ， Hash Table 的實作是 Dict ，而且 Python 的 Dict 有很多好用的 API 可用。

以下列出常見的使用情境

### 計數

#### 算有一個字串中每個字元各有幾個：透過字串的索引

```python
s = 'apple'
table = {}
for i in range(len(s)):
    if s[i] in table:
        table[s[i]] += 1
    else:
        table[s[i]] = 1
print(table)
# {'a': 1, 'p': 2, 'l': 1, 'e': 1}
```

#### 算有一個字串中每個字元各有幾個：直接遍歷字元

```python
s = 'apple'
table = {}
for char in s:
    if char in table:
        table[char] += 1
    else:
        table[char] = 1
print(table)
# {'a': 1, 'p': 2, 'l': 1, 'e': 1}
```

#### 算有一個陣列每個每個字串各有幾個

```python
words = ['apple', 'apple', 'orange', 'banana']
table = {}
for word in words:
    if word in table:
        table[word] += 1
    else:
        table[word] = 1
print(table)
# {'apple': 2, 'orange': 1, 'banana': 1}
```

#### 算有一個陣列中每個每個數字出現幾次

```python
numbers = [random.randint(0, 3) for _ in range(10)]
table = {}
for number in numbers:
    if number in table:
        table[number] += 1
    else:
        table[number] = 1
print(table)
# {0: 2, 2: 4, 1: 2, 3: 2} 
```

上面的技巧其實只要注意到，如果當下的元素還沒有出現在 Table 裡面，我們要預設是 1 ，後面才可以繼續累加上去，不然會發生 Key not found 的情況。

到了這裡，如果已經熟練了 Hash Table ，有三個 API 可以在寫題目的時候，可以讓你寫的程式更少發生小細節寫錯的情況

| API  | 功能 |
| :--- | :--- |
| [`Counter`](https://docs.python.org/3/library/collections.html#collections.Counter) | dict subclass for counting hashable objects |
| [`OrderedDict`](https://docs.python.org/3/library/collections.html#collections.OrderedDict) | dict subclass that remembers the order entries were added |
| [`defaultdict`](https://docs.python.org/3/library/collections.html#collections.defaultdict) | dict subclass that calls a factory function to supply missing values |

計數情況實在很常見，Python 有提供另一個 Library 叫做 [defaultdict](https://docs.python.org/3/library/collections.html#collections.defaultdict) ，可以幫我們做更多的事情，defaultdict 想要解決的是如果我們需要給 Hash Table 一個預設值的時候，我們可以直接指定。

以上的所有例子，都可以這樣改寫，概念比較重要，所以我只用其中一個例子來改寫，我們希望預設的值是 0 。

```python
words = ['apple', 'apple', 'orange', 'banana']
table = defaultdict(int)
for word in words:
    table[word] += 1
print(table)
defaultdict(<class 'int'>, {'apple': 2, 'orange': 1, 'banana': 1})
```

一般來說我們都是用 0 開始，如果想要從 1 開始，可以這樣寫`table = defaultdict(lambda: 1)` 不過這比較少見。

這樣的寫法其實已經很簡潔了，但是 Python 還有提供一個更方便的東西： [Counter](https://docs.python.org/3/library/collections.html#collections.Counter)。

```python
words = ['apple', 'apple', 'orange', 'banana']
counter = collections.Counter(words)
print(counter)
# Counter({'apple': 2, 'orange': 1, 'banana': 1})
```

Hash Table 是可以很彈性的，像是上面的例子，我們知道每個字出現的頻率各是多少後，我們也可以用這個結果去找出每個頻率中，各出現了哪些字。

```python
words = ['apple', 'apple', 'orange', 'banana']
wordToFreq = collections.Counter(words)
freqToWord = collections.defaultdict(list)
for key, val in wordToFreq.items():
    freqToWord[val].append(key)
print(wordToFreq)
# Counter({'apple': 2, 'orange': 1, 'banana': 1})
print(freqToWord)
# defaultdict(<class 'list'>, {2: ['apple'], 1: ['orange', 'banana']})
```

最後一個，是這三個 API 裡面，比較複雜的 Orderdict 。

雖然說 Hash Table 在增、刪、查、改的時間複雜度都很完美，可是 Hash Table 是無序的，我們無法得知每個元素在加入到 Hash Table 時出現的前後順序，因此為了解決這個問題，其實我們可以用一個陣列來把每個元素的位置記錄起來，或是也可以用 Doubly Linked List 來幫我們處理，這樣的處理在查找最早加入或是最晚加入尤其有效率。 在 Java 中，有個 LinkedHashMap 可以完成這個事情，而在 Python 可以自己實作 Linked List ，或是就用 Orderdict 就好。

我一時想不到很好的例子，但是我推薦可以試試看 LeetCode 上面的兩道常考的大魔王， LRU、LFU Cache。

{% page-ref page="../design/cache/lru-cache-zui-jiu-wei-shi-yong-yan-suan-fa.md" %}

{% page-ref page="../design/cache/lfu-cache-zui-jin-zui-shao-shi-yong-yan-suan-fa.md" %}

