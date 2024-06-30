---
title: Races and Mutual Exclusion
---

# Races

What is a race? Let's take for example a simple counter using two threads.
This object counter is shared between the two threads

```java
public class Counter {
    private long value;

public long getAndIncrement() {
    return value++;
}
}
```

The objective of this counter is to print every single prime number until 100. To do that we can write the following code snippet:

```java
int counter = new Counter(1);

void primePrint {
    long j = 0;
    while (j < 100) {
        j = counter.getAndIncrement();
    if (isPrime(j))
    print(j);
}
}
```

Has we know, the variable counter will be shared. To understand why this code may cause some problems we must know a bit about the way a computer works.

When both threads are acessing the same spot in memory, the order in which they write and read is not precise. So there are times where both can read the same thing from the variable `value` but when writing it, it's possible that some time has passed and the `value` may not be the same.

![Imagem](imgs/race-example)

Being said all this, this code is pretty much okay when it comes to single-threaded programs, but for a multi-threaded program this will cause a lot of races. 

# Mutual Exclusion

## Locks

A way to solve this problem is through using **locks**. In Java a lock is define by the following interface:

```java
public interface Lock {
    public void lock(); //acquire lock
    public void unlock(); //release lock
}
```

A way to solve the previous problem using locks can be something like this
```java
public class Counter {
    private long value;
    private Lock lock;


    public long getAndIncrement() {
        lock.lock(); 

        try {
            int temp = value;
            value = value + 1;
        } finally {
            lock.unlock();
        }

        return temp;
    }
}
```

As you can see, the code that needs to be protected from the race (the read and write of value) is inside the `try`. To this code we will call it the *critical section*. What is happening here is that we are locking the shared object (Counter) when doing the method `getAndIncrement()`, this means, the variables in it are only being acessed and altered by one single thread, the other threads can't do anything to it. This way we guarantee that the threads won't read different values or write the wrong value to the object.
