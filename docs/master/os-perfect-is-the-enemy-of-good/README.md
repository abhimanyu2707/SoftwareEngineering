---
description: >-
  Some useful OS concepts mostly Linux related. C code threading would also be
  good
---

# OS (Perfect is the enemy of good!)

* **Page size -** Normally 4KB.
* **Two-Hand clock algorithm -** Cache eviction algorithm where we reset the bits related to all the elements in the cache and set it if it has been accessed. This is done in MMU which takes almost no time. After N seconds the elements for which the bits remain as reset are contenders for eviction.
  * **Pitfall -** If N is low, means a lot of contenders for eviction; If N is high, means not many elements to evict.
  * **Good idea -** No need for a lock on the whole cache, just a lock on the element which is being discarded is enough.
* **Elevator Algorithm -** While reading from slow rotational media(HDD), sort all n read/writes as moving the head takes time and read LBN(logical block number) like an elevator.
* **inode -** Data structure which contains meta-data of a file.
* &#x20;

