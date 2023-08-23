# Synchronisation Examples

## Bounded-Buffer Problem
In this problem, the producer and consumer processes share the following data
structures.

```
int n;
semaphore mutex = 1;
semaphore empty = n;
semaphore full = 0;
```

We assume that the pool consits of `n` buffers, each capable of holding one item.
The `mutex` binary semaphore provides mutual exclusion for accesses to the buffer 
pool and is initialised to the value 1. The `empty` and `full` semaphores count
the number of empty and full buffers. 

```
while (true) {
    // ...
    // Produce an item in next_produced
    // ...

    wait(empty);
    wait(mutex);

    // ...
    // Add next_produced to the buffer
    // ...

    signal(mutex);
    signal(full);
}
```
**Figure: The structure of the producer process.**

```
while (true) {
    wait(full);
    wait(mutex);

    // ...
    // Remove an item from the buffer to next_consumed
    // ...

    signal(mutex);
    signal(empty);

    // ...
    // consume the item in next_consumed
    // ...
}
```
**Figure: The structure of the consumer process.**

We can interpret this code as the producer producing full buffers for the consumer 
or as the consumer producing empty buffers for the producer.

## Readers-Writers Problem
Suppose that the database is to be shared among several concurrent processes.
Some of these processes may want only to read the database (readers), whereas 
others may want to update the database (writers). Two readers can access the 
shared data simultaneously with no adverse effects however, if a writer and some 
other process (either reader or writer) access the data simultaneously, chaos 
may ensure.

To avoid these situations from arising, it's required that the writers have
exclusive access to the shared database while writing to the database. This 
synchronisation problem is referred to as the readers-writers problem. This 
problem has several variations, all involving priorities.

The first readers-writers problem requires that no reader be kept waiting unless 
a writer has already obtained permission to use the shared object. No reader should
wait for other readers to finish simply because a writer is waiting. The second 
readers-writers problem requires that once a writer is ready, that writer peform 
its write as soon as possible. If a writer is waiting to access the object, no 
new readers may start reading. 

A solution to either may result in starvation. In the first case, writers may
starve, in the second case, readers may starve. It's because of this that other
variants of the problem have been proposed.

In the following solution to the first readers-writers problem, the reader processes
share the following data structures:

```
semaphore rw_mutex = 1;
semaphore mutex = 1;
int read_count = 0;
```

The semaphore `rw_mutex` is common to both reader and writer processes. The `mutex`
semaphore is used to ensure mutual exclusion when the variable `read_count` is
updated. The `read_count` variable keeps track of how many process are currently
reading the object. The semaphore `rw_mutex` functions as a mutual exclusion
semaphore for the writers. It is also used by the first or last reader that
enters or exits the critical section. It is not used by readers that enter or 
exit while other readers are in their critical sections.

```
while (true) {
    wait(rw_mutex);

    // ...
    // writing is performed
    // ...

    signal(rw_mutex);
}
```
**Figure: The structure of a writer process.**

```
while (true) {
    wait(mutex);
    read_count++;

    if (read_count == 1) {
        wait(rw_mutex);
    }

    signal(mutex);

    // ...
    // reading is performed
    // ...

    wait(mutex);
    read_count--;

    if (read_count == 0) {
        signal(rw_mutex);
    }

    signal(mutex);
}
```
**Figure:The structure of a reader process.**

## Dining-Philosophers Problem
Consider five philosophers who spend their lives thinking and eating. The philosophers
share a circular table surrounded by five chairs. In the center of the table is
a bowl of rice, and the table is laid with five single chopsticks. When a philosopher
thinks, she does not interact with her colleagues. From time to time, a philosopher 
gets hungry and tries to pick up the two chopsticks that are closest to her 
(the chopsticks that are between her and her left and right neighbors). A philosopher 
may pick up only one chopstick at a time. Obviously, she cannot pick up a chopstick 
that is already in the hand of a neighbor. When a hungry philosopher has both 
her chopsticks at the same time, she eats without releasing the chopsticks. 
When she is finished eating, she puts down both chopsticks and starts thinking 
again. 

This is known as the dining-philosophers problem and is a classic synchronisation
problem because it is an example of a large class of concurrency-control problems.
It is a simple representation of the need to allocate several resources among
several processes in a deadlock-free and starvation-free manner.

```
while (true) {
    wait(chopstick[i]);
    wait(chopstick[(i + 1) % 5]);

    // ...
    // eat for a while
    // ...

    signal(chopstick[i]);
    signal(chopstick[(i + 1) % 5]);

    // ...
    // think for a while
    // ...
}
```
**Figure: The structure of philosopher \\(i\\).**

One simple solution is to represent each chopstick with a semaphore. A philosopher 
tries to grab a chopstick by executing a `wait()` operation on that semaphore. 
She releases her chopsticks by executing the `signal()` operation on the appropriate 
semaphores. Thus, the shared data are

```
semaphore chopstick[5];
```

where all the elements of chopstick are initialized to 1. Although this solution 
guarantees that no two neighbors are eating simultaneously, it could create a 
deadlock. Suppose that all five philosophers become hungry at the same time and 
each grabs her left chopstick. All the elements of chopstick will now be equal 
to 0. When each philosopher tries to grab her right chopstick, she will be delayed 
forever.

Here we presenting a deadlock-free solution to the dining-philosophers problem. 
This solution imposes the restriction that a philosopher may pick up her chopsticks 
only if both of them are available.

```
monitor DiningPhilosophers {
    enum {
        THINKING, 
        HUNGRY, 
        EATING
    } state[5]; 
    condition self[5];

    void pickup(int i) { 
        state[i] = HUNGRY; 
        test(i);

        if (state[i] != EATING) {
            self[i].wait();
        }
    }

    void putdown(int i) { 
        state[i] = THINKING; 
        test((i + 4) % 5); 
        test((i + 1) % 5);
    }

    void test(int i) {
        if ((state[(i + 4) % 5] != EATING) &&
                (state[i] == HUNGRY) &&
                (state[(i + 1) % 5] != EATING) ) {
            state[i] = EATING;
            self[i].signal();
        } 
    }

    initialization code() {
        for (int i = 0; i < 5; i++) {
            state[i] = THINKING;
        }
    } 
}
```
**Figure: A monitor solution to the dining-philosophers problem.**
