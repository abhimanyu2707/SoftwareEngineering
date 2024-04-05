---
description: OS Lecture 26
---

# Producer Consumer

### Pseudocode

```markup
# Initialization
Mutex mutex;          #For mutual exclusion of both
Semaphore empty = N;  #Wait for Producer if no empty
Semaphore full = 0;   #Wait for Consumer if no full
int in = 0;           #index for producer
int out = 0;          #index for consumer
int buffer[N];        #Queue of product.

#Producer
while(True) {
    wait(empty);
    wait(mutex);
    buffer[in] = item;
    in = (in + 1) % N;
    signal(mutex);
    signal(full);     #Signal full as there is an item for the consumer.
}

#Consumer
while(True) {
    wait(full);
    wait(mutex);
    item = buffer[out];
    out = (out + 1) % N;
    signal(mutex);
    signal(empty);
}
```

### C code

* [**https://faculty.cs.niu.edu/\~hutchins/csci480/semaphor.htm**](https://faculty.cs.niu.edu/\~hutchins/csci480/semaphor.htm)
* **sem\_t var :** sem\_t var, sem\_init(\&var, 0/\*shared\*/, \<init\_val>), sem\_wait(\&var), sem\_post(\&var), sem\_destroy(\&var).
* **pthread\_mutex\_t var :** pthead\_mutex\_t var, pthread\_mutex\_init(\&var, NULL/\*attr\*/), pthread\_mutex\_lock(\&var), pthread\_mutex\_unlock(\&var), pthread\_mutex\_destroy(\&var)
* **pthread\_t var:** pthread\_create(\&var, NULL/\*attr\*/, \&function, NULL/\*\<void \* arg>\*/), pthread\_join(var, NULL/\*\<void\*\* thread\_return>\*/

```cpp
//sem_init does not work on OSX, use below commands:
// sem_init -> sem_open
// sem_post is fine
//sem_destroy -> sem_close, sem_unlink
#include<pthread.h>
#include<semaphore.h>
#include<stdlib.h>    //For memory allocation
#include<stdio.h>
#include<unistd.h>
#define MaxItems 5    //Max  a producer can produce and a consumer can consume
                      //It helps to finish the thread.
#define BufferSize 10 //Size of a queue

pthread_mutex_t mutex;
sem_t full;
sem_t empty;
int queue[BufferSize];
int in = 0;
int out = 0;

void* produce(void* pNo) {
    for (int i = 0; i < MaxItems; ++i) {
        int item = rand();
        sem_wait(&empty);
        pthread_mutex_lock(&mutex);
        queue[in] = item;
        printf("Producer %d added item %d at %d\n", *((int*)pNo), item, in);
        in = (in + 1) % BufferSize;
        pthread_mutex_unlock(&mutex);
        sem_post(&full);
    }
    return NULL;
}

void* consume(void* cNo) {
    for (int i = 0; i < MaxItems; ++i) {
        sem_wait(&full);
        pthread_mutex_lock(&mutex);
        int item = queue[out];
        printf("Consumer %d consumed %d at %d\n", *((int*)cNo), item, out);
        out = (out + 1) % BufferSize;
        pthread_mutex_unlock(&mutex);
        sem_post(&empty);
    }
    return NULL;
}

int main() {
    pthread_t producers[5], consumers[5];
    pthread_mutex_init(&mutex, NULL); //Init should ideally be checked for error, 0 means success.
    sem_init(&full, 0, 0);            //arguments are sem_t, int pshared(0 means shared in all thread), initial value
    sem_init(&empty, 0, BufferSize);
    int PC_num[5] = {1, 2, 3, 4, 5};

    for (int i = 0; i < 5; ++i) {
        pthread_create(&producers[i], NULL, &produce, (void *)&PC_num[i]);
    }
    sleep(10);
    for (int i = 0; i < 5; ++i) {
        pthread_create(&consumers[i], NULL, &consume, (void *)&PC_num[i]);
    }
    for (int i = 0; i < 5; ++i) {
        pthread_join(producers[i], NULL);
    }
    for (int i = 0; i < 5; ++i) {
        pthread_join(consumers[i], NULL);
    }
    pthread_mutex_destroy(&mutex);
    sem_destroy(&empty);
    sem_destroy(&full);

    return 0;
}
```
