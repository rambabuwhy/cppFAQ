# Thread-5

#### Problem 1: Producer-Consumer Problem

**Problem:** Implement a solution to the classic producer-consumer problem using C++. The program should have a shared buffer, and multiple producer and consumer threads that safely produce and consume items.

**Code:**

```cpp
#include <iostream>
#include <thread>
#include <mutex>
#include <condition_variable>
#include <queue>

const int BUFFER_SIZE = 5;
std::queue<int> buffer;
std::mutex mtx;
std::condition_variable bufferNotEmpty, bufferNotFull;

void producer(int id) {
    for (int i = 0; i < 10; ++i) {
        std::unique_lock<std::mutex> lock(mtx);
        bufferNotFull.wait(lock, [] { return buffer.size() < BUFFER_SIZE; });

        buffer.push(i);
        std::cout << "Producer " << id << " produced: " << i << std::endl;

        lock.unlock();
        bufferNotEmpty.notify_one();

        std::this_thread::sleep_for(std::chrono::milliseconds(100));
    }
}

void consumer(int id) {
    for (int i = 0; i < 10; ++i) {
        std::unique_lock<std::mutex> lock(mtx);
        bufferNotEmpty.wait(lock, [] { return !buffer.empty(); });

        int item = buffer.front();
        buffer.pop();
        std::cout << "Consumer " << id << " consumed: " << item << std::endl;

        lock.unlock();
        bufferNotFull.notify_one();

        std::this_thread::sleep_for(std::chrono::milliseconds(150));
    }
}

int main() {
    std::thread producer1(producer, 1);
    std::thread producer2(producer, 2);
    std::thread consumer1(consumer, 1);
    std::thread consumer2(consumer, 2);

    producer1.join();
    producer2.join();
    consumer1.join();
    consumer2.join();

    return 0;
}
```

**Explanation:** This problem tests the candidate's ability to use mutexes and condition variables to synchronize multiple producer and consumer threads. The `bufferNotFull` and `bufferNotEmpty` conditions ensure that producers wait when the buffer is full and consumers wait when the buffer is empty, respectively.

***

#### Problem 2: Dining Philosophers Problem

**Problem:** Implement a solution to the dining philosophers problem using C++. The program should have a shared resource (forks) that the philosophers need to eat. Ensure that deadlocks are avoided.

**Code:**

```cpp
#include <iostream>
#include <thread>
#include <mutex>
#include <vector>

const int NUM_PHILOSOPHERS = 5;
std::vector<std::mutex> forks(NUM_PHILOSOPHERS);

void philosopher(int id) {
    int leftFork = id;
    int rightFork = (id + 1) % NUM_PHILOSOPHERS;

    while (true) {
        std::unique_lock<std::mutex> leftLock(forks[leftFork]);
        std::unique_lock<std::mutex> rightLock(forks[rightFork]);

        std::cout << "Philosopher " << id << " is eating." << std::endl;

        leftLock.unlock();
        rightLock.unlock();

        std::this_thread::sleep_for(std::chrono::milliseconds(500));

        std::cout << "Philosopher " << id << " is thinking." << std::endl;

        std::this_thread::sleep_for(std::chrono::milliseconds(500));
    }
}

int main() {
    std::vector<std::thread> philosophers;

    for (int i = 0; i < NUM_PHILOSOPHERS; ++i) {
        philosophers.emplace_back(philosopher, i);
    }

    for (auto& phil : philosophers) {
        phil.join();
    }

    return 0;
}
```

**Explanation:** This problem assesses the candidate's ability to implement a solution to the dining philosophers problem with proper resource (fork) allocation and avoiding deadlocks. The use of unique locks for both forks ensures that each philosopher picks up both forks or releases them atomically.

***

#### Problem 3: Read-Write Lock

**Problem:** Implement a Read-Write lock in C++. Create a shared resource and simulate multiple readers and writers accessing the resource concurrently. Ensure that readers can access the resource simultaneously but exclusive access is provided to writers.

**Code:**

```cpp
#include <iostream>
#include <thread>
#include <shared_mutex>

std::shared_mutex rwMutex;
int sharedData = 0;

void reader(int id) {
    std::shared_lock<std::shared_mutex> lock(rwMutex);
    std::cout << "Reader " << id << " reads sharedData: " << sharedData << std::endl;
}

void writer(int id) {
    std::unique_lock<std::shared_mutex> lock(rwMutex);
    sharedData++;
    std::cout << "Writer " << id << " writes sharedData: " << sharedData << std::endl;
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

**Explanation:** This problem evaluates the candidate's understanding of implementing a Read-Write lock. Readers can concurrently access the shared resource (`sharedData`), while writers require exclusive access. The `std::shared_mutex` provides the necessary synchronization.

#### Problem 4: Bounded Buffer

**Problem:** Implement a bounded buffer with a specified capacity using C++. Create producer and consumer threads that safely produce and consume items from the buffer. Ensure proper synchronization to prevent overflows and underflows.

**Code:**

```cpp
#include <iostream>
#include <thread>
#include <mutex>
#include <condition_variable>
#include <queue>

const int BUFFER_CAPACITY = 5;
std::queue<int> buffer;
std::mutex mtx;
std::condition_variable bufferNotEmpty, bufferNotFull;

void producer(int id) {
    for (int i = 0; i < 10; ++i) {
        std::unique_lock<std::mutex> lock(mtx);
        bufferNotFull.wait(lock, [] { return buffer.size() < BUFFER_CAPACITY; });

        buffer.push(i);
        std::cout << "Producer " << id << " produced: " << i << std::endl;

        lock.unlock();
        bufferNotEmpty.notify_one();

        std::this_thread::sleep_for(std::chrono::milliseconds(100));
    }
}

void consumer(int id) {
    for (int i = 0; i < 10; ++i) {
        std::unique_lock<std::mutex> lock(mtx);
        bufferNotEmpty.wait(lock, [] { return !buffer.empty(); });

        int item = buffer.front();
        buffer.pop();
        std::cout << "Consumer " << id << " consumed: " << item << std::endl;

        lock.unlock();
        bufferNotFull.notify_one();

        std::this_thread::sleep_for(std::chrono::milliseconds(150));
    }
}

int main() {
    std::thread producer1(producer, 1);
    std::thread producer2(producer, 2);
    std::thread consumer1(consumer, 1);
    std::thread consumer2(consumer, 2);

    producer1.join();
    producer2.join();
    consumer1.join();
    consumer2.join();

    return 0;
}
```

**Explanation:** This problem builds on the producer-consumer concept but adds the constraint of a bounded buffer with a specified capacity. The `bufferNotEmpty` and `bufferNotFull` conditions ensure that producers wait when the buffer is full, and consumers wait when the buffer is empty.

***

#### Problem 5: Thread Pool

**Problem:** Implement a simple thread pool in C++. Create a pool of worker threads that execute tasks submitted to the pool. Tasks can be functions or callable objects. Ensure proper synchronization and task execution.

**Code:**

```cpp
#include <iostream>
#include <thread>
#include <queue>
#include <functional>
#include <mutex>
#include <condition_variable>

class ThreadPool {
public:
    ThreadPool(size_t numThreads) : stop(false) {
        for (size_t i = 0; i < numThreads; ++i) {
            workers.emplace_back([this] { workerThread(); });
        }
    }

    ~ThreadPool() {
        {
            std::unique_lock<std::mutex> lock(queueMutex);
            stop = true;
        }
        condition.notify_all();

        for (std::thread& worker : workers) {
            worker.join();
        }
    }

    template<class F, class... Args>
    void enqueue(F&& f, Args&&... args) {
        {
            std::unique_lock<std::mutex> lock(queueMutex);
            tasks.emplace([f = std::forward<F>(f), args = std::make_tuple(std::forward<Args>(args)...)]() {
                std::apply(f, args);
            });
        }
        condition.notify_one();
    }

private:
    std::vector<std::thread> workers;
    std::queue<std::function<void()>> tasks;

    std::mutex queueMutex;
    std::condition_variable condition;
    bool stop;

    void workerThread() {
        while (true) {
            std::unique_lock<std::mutex> lock(queueMutex);

            condition.wait(lock, [this] { return stop || !tasks.empty(); });

            if (stop && tasks.empty()) {
                return;
            }

            auto task = std::move(tasks.front());
            tasks.pop();

            lock.unlock();

            task();
        }
    }
};

void exampleTask(int id) {
    std::cout << "Task executed by thread " << id << std::endl;
}

int main() {
    ThreadPool pool(3);

    for (int i = 0; i < 10; ++i) {
        pool.enqueue(exampleTask, i);
    }

    return 0;
}
```

**Explanation:** This problem tests the candidate's ability to implement a simple thread pool. The `ThreadPool` class manages a pool of worker threads that execute tasks submitted to the pool. Proper synchronization is ensured to handle task execution and pool shutdown.

***

####
