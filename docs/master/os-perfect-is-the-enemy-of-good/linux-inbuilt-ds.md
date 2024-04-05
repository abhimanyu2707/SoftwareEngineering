---
description: >-
  OS code prefers simple data structures and algorithms: easy to dev and debug,
  easier locking semantics (TBD), and a small footprint. The most popular data
  structures are lists and hashes.
---

# Linux Inbuilt DS

* There are some tree structs (B-tree, B+, red-black) but they're used in specific modules as needed.
* Implementing DS is hard, as there could be some pointer bugs introduced.
* Header - **\<linux/list.h>**
* Need to put **"struct list\_head"** inside any structure where it has to be used.
* Can create multiple lists of the same nodes like for LRU, or write-back list for pending write.

```c
```
