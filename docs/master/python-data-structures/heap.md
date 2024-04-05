---
description: Use package heapq
---

# Heap

### heapq

```python
import heapq
h = []

#Min-Heap by default
heapq.heapify(h) #n
heapq.heappush(h, 10) #log(n)
heapq.heappop(h) #log(n)
heapq.heappushpop(h, 20) #log(n)
heapq.nlargest(n, h, key=None)
```
