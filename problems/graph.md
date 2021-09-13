# Graph

## Disjoint Set

### 

{% tabs %}
{% tab title="Quick Find" %}
```python
class UnionFind:
    def __init__(self, size):
        self.root = [i for i in range(size)]
        
    def find(self, x):
        return self.root[x]
    
    def union(self, x, y):
        rootX = self.find(x)
        rootY = self.find(y)
        if rootX != rootY:    
            for i in range(len(self.root)):
                # 使用 rootX 當作新的根節點
                # 找到節點是以 rootY 當作根節點的，就替換成 rootX
                if self.root[i] == rootY:
                    self.root[i] = rootX

    def connected(self, x, y):
        return self.find(x) == self.find(y)
```
{% endtab %}

{% tab title="Quick Union" %}
```python
class UnionFind:
    def __init__(self, size):
        self.root = [i for i in range(size)]
        
    def find(self, x):
        # 不斷的往上尋找，直到找到根節點
        while self.root[x] != x:
            x = self.root[x]
        return x
    
    def union(self, x, y):
        rootX = self.find(x)
        rootY = self.find(y)
        # 如果兩個跟節點不相同，選擇 rootX 當作新的根節點。
        if rootX != rootY:
            self.root[rootY] = rootX        
    
    def connected(self, x, y):
        return self.find(x) == self.find(y)
```
{% endtab %}

{% tab title="Union By Rank" %}
```python
class UnionFind:
    def __init__(self, size):
        self.root = [i for i in range(size)]
        self.rank = [i for i in range(size)]
    
    def find(self, x):
        while self.root[x] != x:
            x = self.root[x]
        return x
    
    def union(self, x, y):
        rootX = self.find(x)
        rootY = self.find(y)
        if rootX != rootY:
            if self.rank[rootX] > self.rank[rootY]:
                self.root[rootY] = rootX
            elif self.ranke[rootX] < self.rank[rootY]
                self.root[rootX] = rootY
            else:
                self.root[rootY] = rootX
                self.rank[rootX] += 1

    def connected(self, x, y):
        return self.find(x) == self.find(y)
```
{% endtab %}

{% tab title="Union Path Compression" %}
```python
class UnionFind:
    def __init__(self, size):
        self.root = [i for i in range(size)]
        
    def find(self, x):
        if x == self.root[x]:
            return x
        self.root[x] = self.find(self.root[x])
        return self.root[x]
    
    def union(self, x, y):
        rootX = self.find(x)
        rootY = self.find(y)
        if rootX != rootY:
            self.root[rootY] = rootX        
    
    def connected(self, x, y):
        return self.find(x) == self.find(y)
```
{% endtab %}

{% tab title="Union Path Compression + Rank" %}


```python
class UnionFind:
    def __init__(self, size):
        self.root = [i for i in range(size)]
        self.rank = [i for i in range(size)]
        
    def find(self, x):
        if x == self.root[x]:
            return x
        self.root[x] = self.find(self.root[x])
        return self.root[x]
    
    def union(self, x, y):
        rootX = self.find(x)
        rootY = self.find(y)
        if rootX != rootY:
            if self.rank[rootX] > self.rank[rootY]:
                self.root[rootY] = rootX
            elif self.ranke[rootX] < self.rank[rootY]
                self.root[rootX] = rootY
            else:
                self.root[rootY] = rootX
                self.rank[rootX] += 1        
    
    def connected(self, x, y):
        return self.find(x) == self.find(y)
```
{% endtab %}
{% endtabs %}

