# Thread-6

#### Problem 6: Single Instance

**Problem:** Implement a mechanism to ensure that only a single instance of a class can be created across multiple threads using C++. Ensure that the instance is lazily initialized and thread-safe.

**Code:**

```cpp
#include <iostream>
#include <mutex>

class Singleton {
private:
    Singleton() {} // Private constructor

public:
    static Singleton& getInstance() {
        static Singleton instance;
        return instance;
    }
};

int main() {
    Singleton& obj1 = Singleton::getInstance();
    Singleton& obj2 = Singleton::getInstance();

    std::cout << "obj1 address: " << &obj1 << std::endl;
    std::cout << "obj2 address: " << &obj2 << std::endl;

    return 0;
}
```

**Explanation:** This problem assesses the candidate's understanding of the singleton pattern and thread-safe lazy initialization. The `Singleton` class ensures that only one instance is created, and the `getInstance` method provides a thread-safe way to access it.

#### Problem 7: Readers-Writers Problem with Priority

**Problem:** Extend the classic Readers-Writers problem by adding priority to writers. Ensure that writers have priority over readers, i.e., no new readers are allowed to start reading when a writer is waiting.

**Code:**

```cpp
#include <iostream>
#include <thread>
#include <shared_mutex>
#include <mutex>

std::shared_mutex rwMutex;
std::mutex priorityMutex;
int sharedData = 0;

void reader(int id) {
    {
        std::unique_lock<std::mutex> lock(priorityMutex);
        rwMutex.lock_shared();
        // Reading sharedData
        std::cout << "Reader " << id << " reads sharedData: " << sharedData << std::endl;
    }
    rwMutex.unlock_shared();
}

void writer(int id) {
    {
        std::unique_lock<std::mutex> lock(priorityMutex);
        rwMutex.lock();
        // Writing sharedData
        sharedData++;
        std::cout << "Writer " << id << " writes sharedData: " << sharedData << std::endl;
    }
    rwMutex.unlock();
}

int main() {
    std::vector<std::thread> readers, writers;

    for (int i = 0; i < 5; ++i) {
        readers.emplace_back(reader, i);
        writers.emplace_back(writer, i);
    }

    for (auto& readerThread : readers) {
        readerThread.join();
    }

    for (auto& writerThread : writers) {
        writerThread.join();
    }

    return 0;
}
```

**Explanation:** This problem extends the Readers-Writers problem by adding a priority mechanism. Writers have priority over readers, ensuring that no new readers start reading when a writer is waiting.

***

#### Problem 8: Parallel Merge Sort

**Problem:** Implement a parallel version of the merge sort algorithm using C++. Use multiple threads to speed up the sorting process.

**Code:**

```cpp
#include <iostream>
#include <vector>
#include <thread>
#include <algorithm>

const int THRESHOLD = 1000;

void merge(std::vector<int>& arr, int low, int mid, int high) {
    std::vector<int> merged(high - low + 1);
    int i = low, j = mid + 1, k = 0;

    while (i <= mid && j <= high) {
        if (arr[i] < arr[j]) {
            merged[k++] = arr[i++];
        } else {
            merged[k++] = arr[j++];
        }
    }

    while (i <= mid) {
        merged[k++] = arr[i++];
    }

    while (j <= high) {
        merged[k++] = arr[j++];
    }

    std::copy(merged.begin(), merged.end(), arr.begin() + low);
}

void parallelMergeSort(std::vector<int>& arr, int low, int high, int depth) {
    if (low < high) {
        if (depth == 0 || high - low < THRESHOLD) {
            std::sort(arr.begin() + low, arr.begin() + high + 1);
        } else {
            int mid = (low + high) / 2;

            std::thread t1(parallelMergeSort, std::ref(arr), low, mid, depth - 1);
            std::thread t2(parallelMergeSort, std::ref(arr), mid + 1, high, depth - 1);

            t1.join();
            t2.join();

            merge(arr, low, mid, high);
        }
    }
}

int main() {
    std::vector<int> data = {5, 2, 9, 1, 5, 6};
    parallelMergeSort(data, 0, data.size() - 1, 2);

    std::cout << "Sorted Array: ";
    for (int num : data) {
        std::cout << num << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

**Explanation:** This problem tests the candidate's understanding of parallel programming by implementing a parallel version of the merge sort algorithm. The `parallelMergeSort` function recursively divides the array into subproblems, and parallel threads are used for sorting and merging.

***

#### Problem 9: Lock-Free Stack

**Problem:** Implement a lock-free stack using C++. The stack should support push, pop, and isEmpty operations, and multiple threads should be able to access it concurrently without locks.

**Code:**

```cpp
#include <iostream>
#include <atomic>
#include <thread>

template <typename T>
class LockFreeStack {
private:
    struct Node {
        T data;
        Node* next;
        Node(T val) : data(val), next(nullptr) {}
    };

    std::atomic<Node*> top;

public:
    LockFreeStack() : top(nullptr) {}

    void push(T val) {
        Node* newNode = new Node(val);
        newNode->next = top.load(std::memory_order_relaxed);

        while (!top.compare_exchange_weak(newNode->next, newNode, std::memory_order_release, std::memory_order_relaxed))
            continue;
    }

    bool pop(T& val) {
        Node* oldTop = top.load(std::memory_order_acquire);
        while (oldTop && !top.compare_exchange_weak(oldTop, oldTop->next, std::memory_order_relaxed))
            continue;

        if (oldTop) {
            val = oldTop->data;
            delete oldTop;
            return true;
        } else {
            // Stack is empty
            return false;
        }
    }

    bool isEmpty() const {
        return top.load(std::memory_order_relaxed) == nullptr;
    }
};

int main() {
    LockFreeStack<int> stack;

    stack.push(42);
    stack.push(55);

    int val;
    if (stack.pop(val)) {
        std::cout << "Popped value: " << val << std::endl;
    }

    return 0;
}
```

**Explanation:** This problem assesses the candidate's understanding of lock-free data structures. The `LockFreeStack` class implements a stack that can be accessed concurrently by multiple threads without the need for locks.

***

#### Problem 10: Deadlock Avoidance

**Problem:** Write a program that demonstrates a potential deadlock situation and then modify it to avoid the deadlock while maintaining the original functionality.

**Code:**

```cpp
#include <iostream>
#include <thread>
#include <mutex>

std::mutex mutex1, mutex2;

void potentialDeadlock() {
    std::unique_lock<std::mutex> lock1(mutex1);
    std::cout << "Thread " << std::this_thread::get_id() << " acquired mutex1." << std::endl;

    std::this_thread::sleep_for(std::chrono::milliseconds(100));

    std::unique_lock<std::mutex> lock2(mutex2);
    std::cout << "Thread " << std::this_thread::get_id() << " acquired mutex2." << std::endl;
}

void deadlockAvoidance() {
    std::unique_lock<std::mutex> lock1(mutex1, std::defer_lock);
    std::unique_lock<std::mutex> lock2(mutex2, std::defer_lock);
    std::lock(lock1, lock2);

    std::cout << "Thread " << std::this_thread::get_id() << " acquired both mutexes." << std::endl;
}

int main() {
    std::thread potentialDeadlockThread1(potentialDeadlock);
    std::thread potentialDeadlockThread2(potentialDeadlock);

    potentialDeadlockThread1.join();
    potentialDeadlockThread2.join();

    std::thread avoidanceThread1(deadlockAvoidance);
    std::thread avoidanceThread2(deadlockAvoidance);

    avoidanceThread1.join();
    avoidanceThread2.join();

    return 0;
}
```

**Explanation:** This problem assesses the candidate's understanding of deadlock situations and their ability to modify code to avoid deadlocks. The first part of the code demonstrates a potential deadlock, and the second part provides a modification to avoid the deadlock while maintaining the original functionality.
