# Detail - 5

## Locks

In C++, locks are used to synchronize access to shared resources in a multithreaded environment. Different types of locks provide different levels of control and efficiency. Here are three commonly used locks: `std::mutex`, `std::unique_lock`, and `std::lock_guard`.

1. **std::mutex (Mutex):**
   * The most basic lock in C++. It provides exclusive ownership to a single thread at a time.

```cpp
#include <iostream>
#include <thread>
#include <mutex>

std::mutex mtx; // mutex for critical section

void sharedResourceFunction(int id) {
    std::unique_lock<std::mutex> lock(mtx); // lock the mutex

    // Critical section
    std::cout << "Thread " << id << " is accessing the shared resource." << std::endl;

    // The mutex will be automatically released when the lock goes out of scope.
}

int main() {
    const int numThreads = 5;
    std::thread threads[numThreads];

    for (int i = 0; i < numThreads; ++i) {
        threads[i] = std::thread(sharedResourceFunction, i);
    }

    for (int i = 0; i < numThreads; ++i) {
        threads[i].join();
    }

    return 0;
}
```

2. **std::unique\_lock:**
   * More flexible than `std::lock_guard`. It allows manual locking and unlocking.

```cpp
#include <iostream>
#include <thread>
#include <mutex>

std::mutex mtx; // mutex for critical section

void sharedResourceFunction(int id) {
    std::unique_lock<std::mutex> lock(mtx);

    // Critical section
    std::cout << "Thread " << id << " is accessing the shared resource." << std::endl;

    // The mutex can be manually unlocked before going out of scope.
    // lock.unlock();
}

int main() {
    const int numThreads = 5;
    std::thread threads[numThreads];

    for (int i = 0; i < numThreads; ++i) {
        threads[i] = std::thread(sharedResourceFunction, i);
    }

    for (int i = 0; i < numThreads; ++i) {
        threads[i].join();
    }

    return 0;
}
```

3. **std::lock\_guard:**
   * Simple lock that automatically locks and unlocks the provided mutex.

```cpp
#include <iostream>
#include <thread>
#include <mutex>

std::mutex mtx; // mutex for critical section

void sharedResourceFunction(int id) {
    std::lock_guard<std::mutex> lock(mtx); // automatically locks and unlocks

    // Critical section
    std::cout << "Thread " << id << " is accessing the shared resource." << std::endl;

    // lock is automatically released when it goes out of scope
}

int main() {
    const int numThreads = 5;
    std::thread threads[numThreads];

    for (int i = 0; i < numThreads; ++i) {
        threads[i] = std::thread(sharedResourceFunction, i);
    }

    for (int i = 0; i < numThreads; ++i) {
        threads[i].join();
    }

    return 0;
}
```

In all examples, multiple threads call the `sharedResourceFunction`, and the use of locks ensures that only one thread at a time can access the critical section (shared resource). This helps avoid race conditions and ensures data integrity in a multithreaded environment.\
