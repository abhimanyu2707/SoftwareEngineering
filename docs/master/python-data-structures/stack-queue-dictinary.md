---
description: 'Stack can be created by normal array; Queue - deque; Some useful dictionaries:'
---

# stack queue dictinary

### collections

[`deque`](https://docs.python.org/3/library/collections.html#collections.deque)`,` [`defaultdict`](https://docs.python.org/3/library/collections.html#collections.defaultdict)`,`[`Counter`](https://docs.python.org/3/library/collections.html#collections.Counter)`,` [`OrderedDict`](https://docs.python.org/3/library/collections.html#collections.OrderedDict)

* **deque**

```python
from collections import deque
d = deque()
d.append(10)
d.popleft()
```

* **defaultdict**

```python
from collections import defaultdict
d = defaultdict(list)
d['k'].append(1)
d['k'].append(2)
```

* **Counter**

```python
s = 'anonymous'
counts = collections.Counter(s)
```

* **OrderedDict**

```python
from collections import OrderedDict
d = OrderedDict(int)
d.popitem(last=True) #O(1) LIFO
d.popitem(last=False) #O(1) FIFO
d.move_to_end(key, last=True) #O(1) DLL
d.move_to_end(key, last=False) #moves the item to front.
for k, v in d.items():
    print(k, v)
```
