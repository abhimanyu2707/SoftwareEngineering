---
description: Starvation |
---

# 😊 Locking

### Types of lock

#### Based on concepts

* Exclusive - Only one lock owner for the critical section (CS)
* Non-exclusive - Limited or unlimited owner.
* Blocking - Scheduler goes to WAITING state. I/O blocking.
* Non-blocking - For small code. Like spinlock.

#### Some pitfalls

* A function tries to take the same lock again, ex rename files in the same directory. It results in a Deadlock. **Resolution: Compare the variables with which the locks are associated.**
* The order of locks should remain same or two treads will be in deadlock waiting for others to release the lock. **Resolution: Put locks on variables with a lesser value first (a deterministic order).**
* Sometimes multithreading results in an undefined state based on the race winner. The best practice is to serialize such cases. **e.g. renaming a folder in Linux.**
* **Always free the lock before returning from the function.**
* **Use mutex if you want to sleep on being idle.**
* Avoid using kmalloc in cases like reader-writer/producer-consumer. And limit the size of the waiting queue.

#### &#x20;Based on implementation

* **spinlock\_t** - For non-blocking small CS. It is implemented using an infinite loop.
* **struct mutex** - Mutually exclusive lock. The loser waits in the WAITING state unless something wakes it up.
* **atomic\_t** - It is typedef for **struct atomic\_counter,** which can be used for ref-count. It uses mutex. There is a variant with a spin lock. APIs are: **atomic\_read, atomic\_set, atomic\_inc**
* **rwsem** (read write semaphore) - It is non exclusive, as it allows multiple read and only one writer. APIs are: **lock\_read, unlock\_read, lock\_write, unlock\_write.**
* **rcu** (read-copy-update) - This can allow long critical sections, but the user has to take care of the updates. Version is used to control fast merge. IMO git uses this lock.

### Concurrency in c

```c
#include <linux/list.h> //List class
#include<pthread.h>
#include<semaphore.h>

pthread_t thread;
pthread_create(&thread, NULL/*attr*/, &function, NULL/*<void * arg>*/);
pthread_join(thread, NULL/*<void** thread_return>*/);

pthread_mutex_t m_lock;
pthread_mutex_init(&m_lock, NULL/*attr*/);
pthread_mutex_lock(&m_lock);
//CS
pthread_mutex_unlock(&m_lock);
pthread_mutex_destroy(&m_lock);

sem_t lock;
sem_init(&lock, 0/*shared*/, <init_val>);
sem_wait(&var);
//CS
sem_post(&var);
sem_destroy(&var)

//Linux:
atomic_t len;
atomic_set(&len, 0);
atomic_read(&len);
atomic_inc(&len);
```

### Concurrency in c++

* [https://leetcode.com/problems/web-crawler-multithreaded/](https://leetcode.com/problems/web-crawler-multithreaded/)
* [https://www.codeproject.com/Articles/598695/Cplusplus11-Threads-Locks-and-Condition-Variables](https://www.codeproject.com/Articles/598695/Cplusplus11-Threads-Locks-and-Condition-Variables)

```c
#include<thread>
#include<mutex>
#include<condition_variable>    //For Monitor
#include <chrono>               //For time

std::thread th(func, args);     //Arguments are copied, for reference use std::ref()
th.join();
th.detach()                     //Can't be joined as it is a separate execution.
//Helper functions to run inside thread.
std::this_thread::get_id();
std::this_thread::sleep_for(std::chrono::seconds(<int>));

//Primitive mutex
std::mutex _lock;
_lock.lock();
_lock.unlock();
std::recursive_mutex _lock;    //Same thread can call lock and unlock multiple times.

//RAII over mutex (Resource Acquisition is Initialization)
{
    std::lock_guard<std::mutex> locker(_lock);   //gets locked on creation
    //CS
}   //gets unlocked when the destructor is called

//unique_lock wrapper has more functionality
{
    std::unique_lock<std::recursive_mutex> locker(_lock); //locks instantly.
    std::unique_lock<std::mutex> locker(_lock, std::deferred_lock); //need locking, std::adopt_lock is used if already has the ownership.
    
    locker.lock();
    //OR
    std::lock(locker, locker2); //To avoid deadlock
}

```
