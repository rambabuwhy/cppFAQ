# Thread-2

#### 11. **What is a race condition, and how can it be addressed using atomic operations?**

*   **Code:**

    ```cpp
    #include <iostream>
    #include <thread>
    #include <atomic>

    std::atomic<int> counter(0);

    void increment() {
        for (int i = 0; i < 100000; ++i) {
            counter.fetch_add(1, std::memory_order_relaxed);
        }
    }

    int main() {
        std::thread t1(increment);
        std::thread t2(increment);

        t1.join();
        t2.join();

        std::cout << "Counter value: " << counter << std::endl;
        return 0;
    }
    ```
* **Explanation:** This question focuses on using `std::atomic` and its `fetch_add` operation to perform atomic increments without the need for locks.

#### 12. **Explain the concept of a mutex and how it helps in achieving mutual exclusion.**

* **Explanation:** A mutex (mutual exclusion) is used to protect shared resources from concurrent access by multiple threads. Only one thread can lock the mutex at a time, ensuring mutual exclusion.

#### 13. **What are the advantages and disadvantages of using locks in concurrent programming?**

* **Explanation:** This question assesses the candidate's understanding of the trade-offs involved in using locks, including advantages such as simplicity and disadvantages such as potential for deadlocks and performance overhead.

#### 14. **What is the purpose of the `std::unique_lock` class, and how does it differ from `std::lock_guard`?**

*   **Code:**

    ```cpp
    #include <iostream>
    #include <thread>
    #include <mutex>

    std::mutex mtx;

    void criticalSection() {
        std::unique_lock<std::mutex> lock(mtx);
        // Critical section code
    }

    int main() {
        std::thread t(criticalSection);
        t.join();
        return 0;
    }
    ```
* **Explanation:** `std::unique_lock` is more flexible than `std::lock_guard` as it allows for deferred locking and timed locking. It is used to guard critical sections of code.

#### 15. **How can you achieve parallelism in C++ using std::async and std::future?**

*   **Code:**

    ```cpp
    #include <iostream>
    #include <future>

    int square(int x) {
        return x * x;
    }

    int main() {
        std::future<int> result = std::async(std::launch::async, square, 5);
        std::cout << "Result: " << result.get() << std::endl;
        return 0;
    }
    ```
* **Explanation:** `std::async` can be used to execute a function asynchronously, and `std::future` is used to retrieve the result once the asynchronous operation is complete.

#### 16. **Explain the concept of a semaphore and its role in synchronization.**

*   **Code:**

    ```cpp
    #include <iostream>
    #include <thread>
    #include <mutex>
    #include <condition_variable>

    std::mutex mtx;
    std::condition_variable cv;
    int resourceCount = 0;

    void producer() {
        {
            std::unique_lock<std::mutex> lock(mtx);
            resourceCount++;
        }
        cv.notify_one();
    }

    void consumer() {
        std::unique_lock<std::mutex> lock(mtx);
        cv.wait(lock, [] { return resourceCount > 0; });
        resourceCount--;
    }

    int main() {
        std::thread t1(producer);
        std::thread t2(consumer);

        t1.join();
        t2.join();

        return 0;
    }
    ```
* **Explanation:** This question explores the candidate's understanding of semaphores and how they can be implemented using mutex and condition variables to control access to shared resources.

#### 17. **What is the purpose of the `std::condition_variable_any` class in C++?**

* **Explanation:** `std::condition_variable_any` is a more flexible alternative to `std::condition_variable` that can work with any lock type.

#### 18. **How does the "Happens-Before" relationship relate to memory ordering in C++?**

* **Explanation:** The "Happens-Before" relationship is a concept in C++ memory ordering that defines the order of visibility of memory operations between threads. Understanding this relationship is crucial for writing correct concurrent code.

#### 19. **Explain the concept of a reader-writer lock and its use cases.**

*   **Code:**

    ```cpp
    #include <iostream>
    #include <thread>
    #include <shared_mutex>

    std::shared_mutex rwMutex;
    int sharedData = 0;

    void reader() {
        std::shared_lock<std::shared_mutex> lock(rwMutex);
        std::cout << "Read sharedData: " << sharedData << std::endl;
    }

    void writer() {
        std::unique_lock<std::shared_mutex> lock(rwMutex);
        sharedData++;
        std::cout << "Write sharedData: " << sharedData << std::endl;
    }

    int main() {
        std::thread t1(reader);
        std::thread t2(writer);

        t1.join();
        t2.join();

        return 0;
    }
    ```
* **Explanation:** This question checks the candidate's understanding of reader-writer locks and their application in scenarios where multiple threads need to read a shared resource concurrently, but writing requires exclusive access.

#### 20. **What is a condition variable spurious wake-up, and how can it be handled?**

* **Explanation:** A spurious wake-up occurs when a thread is awakened from its waiting state even though no corresponding `notify` or `notify_all` signal was sent. Handling spurious wake-ups usually involves checking a condition after waking up to verify if the expected state has been reached.
