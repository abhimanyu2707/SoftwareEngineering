---
description: >-
  Inside linux clone() is the base class called by fork and pthread_create with
  different flags to share different resources like working directory, files &
  locks.
---

# Process & Thread

### Some Thoughts:

* You can create your own clone() with different flags. But also need to clear data from RAM so that it does not give Kernel crash.
* COW - Copy on write. In the case of fork avoids copying till a write is performed.

### Important Links:

* [https://stackoverflow.com/questions/807506/threads-vs-processes-in-linux](https://stackoverflow.com/questions/807506/threads-vs-processes-in-linux)
* [Making legacy code thread-safe](https://www.wesleysteiner.com/professional/MakingLegacyCodeSafe.html)
* [C++ Thread and Locking.](https://www.codeproject.com/Articles/598695/Cplusplus11-Threads-Locks-and-Condition-Variables)

### C++ Threads

* static variable can be declared per thread using **"thread\_local int var = 0"**
*
