---
sort: 4
---

# Multithreading

in python we are not making a list of threads then create each one of them as in c++, just create.

```python
import threading

def func(parm):
    print("Hello World!")


if __name__ == "__main__":

    x = threading.Thread(target=func, args=(1,))

    x.start()

    x.join()
```

## Daemon Threads ?? 
In computer science, a daemon is a process that runs in the background.

In Python A daemon thread will shut down immediately when the program exits

If a program is running Threads that are <bold>not</bold> daemons, then the program will wait for those threads to complete before it terminates

If you look at the source for Python threading, you’ll see that threading._shutdown() walks through all of the running threads and calls .join() on every one that does not have the daemon flag set.

```python
x = threading.Thread(target=func, args=(1,), daemon=True)
```



## ThreadPool

```python
import concurrent.futures   

def func(parm):
    print("Hello World!")

if __name__ == "__main__":

    with concurrent.futures.ThreadPoolExecutor(max_workers=3) as executor:
        executor.map(object.method(parm1, ...), range(3))
```

The code creates a ThreadPoolExecutor as a context manager, telling it how many worker threads it wants in the pool. It then uses .map() to step through an iterable of things, in your case range(3), passing each one to a thread in the pool.

The end of the with block causes the ThreadPoolExecutor to do a .join() on each of the threads in the pool. It is strongly recommended that you use ThreadPoolExecutor as a context manager when you can so that you never forget to .join() the threads.


## Race Conditions & Locks

```python
class FakeDatabase:
    def __init__(self):
        self.value = 0                  # Conseder it Global between threads
        self.lock = threading.Lock()
        # OR
        self.mutex = threading.Semaphore()

    def locked_update(self):
        with self.lock:
            self.value += 1


    def locked_update2(self):
        self.lock.acquire()
        self.value += 1
        self.lock.release()


    def locked_update3(self):
        self.mutex.acquire()
        self.value += 1 
        self.mutex.release()
```




# Timer
```python
t = threading.Timer(30.0, func)
```

# Barrier


# producer-consumer-problem

https://www.askpython.com/python/producer-consumer-problem