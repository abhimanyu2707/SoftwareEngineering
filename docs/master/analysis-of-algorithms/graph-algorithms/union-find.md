---
description: Union-Find Algorithm using Disjoint Set
---

# Union-Find

* Can be used to detect cycle
* Used in Kruskal's algorithm to create MST.

### 1. Only Path Compression

#### Python Code

```python
class UF:
    def __init__(self, n):
        self.size = n #number of distinct graph or set
        self.parent = [i for i in range(n)]
        
    def union(self, x, y):
        self.link(self.find(x), self.find(y))
        
    def link(self, x, y):
        if x == y:
            return
        self.size -= 1
        self.parent[y] = x
    
    def find(self, x):
        if x != self.parent[x]:
            self.parent[x] = self.find(self.parent[x])
        return self.parent[x]
```

### 2. Rank and Path Compression

Using Union by Rank and Path Compression - Rank is stored for each element to make the larger tree the parent of the smaller tree. A Tree is nothing but a structure which gets created while creating a set.

#### Algorithm

```markup
MAKE_SET(x):
    x.parent = x
    x.rank = 0
    
UNION(x, y):
    LINK(FIND_SET(x), FIND_SET(y))
    
LINK(x, y):
    if x.rank > y.rank:
        y.parent = x
    else:
        x.parent = y
        if x.rank == y.rank:
            y.rank = y.rank + 1

#FIND_SET with path compression
FIND_SET(x):
    if x.parent != x:
        x.parent = FIND_SET(x.parent)
    return x.parent
    
```

#### Python Code

```python
class UF:
    def __init__(self, n):
        self.size = n
        self.parent = [i for i in range(n)]
        self.rank = [0 for _ in range(n)]
        
    def union(self, x, y):
        self.link(self.find(x), self.find(y))
        
    def link(self, x, y):
        if x == y:
            return
        self.size -= 1
        if self.rank[x] > self.rank[y]:
            self.parent[y] = x
        else:
            self.parent[x] = y
            if self.rank[x] == self.rank[y]:
                self.rank[y] += 1
    
    def find(self, x):
        if x != self.parent[x]:
            self.parent[x] = self.find(self.parent[x])
        return self.parent[x]
```

#### Time Complexity

O(m\*constant) where m is the number of times the union is called. Union takes amortized constant time when rank and compression are used.
