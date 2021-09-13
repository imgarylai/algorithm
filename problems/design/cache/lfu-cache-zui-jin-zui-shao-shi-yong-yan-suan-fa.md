# LFU Cache 最近最少使用演算法

LFU 則是另外一個快取機制，主要是讓越常被存取的資料更快地取出，並包含 LRU 的機制，如果超過限制的資源，把最少用掉的刪掉，如果最少用到的資料取出的頻率相同時，則優先刪除更早以前的資料。

所以我們至少需要知道的東西有兩件

1. 每筆資料分別的使用頻率
2. 每筆資料分別進入的順序（當遇上同樣頻率時，選擇哪個要優先刪除）

所以最少我們需要的有兩樣東西，第一個是 `key_to_freq` 這用來記錄每一個資料的頻率，至於順序重不重要呢？我先想了想，應該是不重要，所以用一般的 Hash Table 就好了。

第二個是 `freq_to_keys` ，這裡需要花一點時間理解，我們需要紀錄每一種頻率，各有哪幾筆資料被送進來過，如果是一個陣列的話足夠嗎？應該不足夠，舉例來說，如果我們呼叫一次 `get` 而要造訪的資料在中間的話，我們還需要有另一個 Hash Table 來記錄去紀錄每個位置，不然的話沒辦法記錄著位子，但是光是這樣還不夠，我們還有數值要儲存，所以 LRU 利用到的 Doubly Linked List + Hash Map 在這裡就可以用得到了。這裡為了方便，就直接使用了 `OrderedDict` 來記錄。

新增資料時，如果資料沒有存在過其實還算簡單，這題目難是難在新增資料時資料已經存在，以及查詢資料時，因為我們需要更新這筆資料的造訪頻率以及排序好這筆資料的位置（移動到最後）

使用的方式如下，每次查找資料的時候先從`key_to_freq` 找到這個 key 的 frequency ，然後該 frequency 於 `freq_to_keys` 的資料，然後該筆資料會是一個 OrderedDict ，我們此時就可以找到該值的 value 。

```python
class LFUCache:
    def __init__(self, capacity: int):
        self.capacity = capacity
        self.key_to_freq = collections.defaultdict()
        self.freq_to_keys = collections.defaultdict(collections.OrderedDict)
        self.minfreq = 0
```

```python
class LFUCache:
    def __init__(self, capacity: int):
        self.capacity = capacity
        self.key_to_freq = collections.defaultdict()
        self.freq_to_keys = collections.defaultdict(collections.OrderedDict)
        self.minfreq = 0    

    def get(self, key: int) -> int:
        if key not in self.key_to_freq:
            return -1
        freq = self.key_to_freq[key]
        val = self.freq_to_keys[freq][key]
        del self.freq_to_keys[freq][key]
        if not self.freq_to_keys[freq]:
            del self.freq_to_keys[freq]
            if freq == self.minfreq:
                self.minfreq += 1
        self.key_to_freq[key] = freq+ 1
        self.freq_to_keys[freq+1][key] = val
        return val

    def put(self, key: int, value: int) -> None:
        if self.capacity <= 0: return
        if key in self.key_to_freq:
            freq = self.key_to_freq[key]
            self.freq_to_keys[freq][key] = value
            # update freq
            self.get(key)
        else:
            if self.capacity == len(self.key_to_freq):
                delkey, delval = self.freq_to_keys[self.minfreq].popitem(last=False)
                del self.key_to_freq[delkey]
            self.key_to_freq[key] = 1
            self.freq_to_keys[self.key_to_freq[key]][key] = value
            self.minfreq = 1
```

