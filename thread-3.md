# Thread-3

#### 21. **What is the ABA problem in concurrent programming, and how can it be mitigated?**

* **Explanation:** The ABA problem occurs when a value changes from A to B and back to A, making it challenging to detect changes. Techniques such as using atomic compare-and-swap (CAS) operations with additional tags can help mitigate the ABA problem.

#### 22. **Explain the concept of thread-local storage (TLS) in C++.**

*   **Code:**

    ```cpp
    #include <iostream>
    #include <thread>

    thread_local int threadSpecificData = 0;

    void threadFunction() {
        threadSpecificData++;
        std::cout << "Thread-specific data: " << threadSpecificData << std::endl;
    }

    int main() {
        std::thread t1(threadFunction);
        std::thread t2(threadFunction);

        t1.join();
        t2.join();

        return 0;
    }
    ```
* **Explanation:** Thread-local storage allows each thread to have its own instance of a variable. It is declared using the `thread_local` keyword.

#### 23. **What is the difference between optimistic and pessimistic concurrency control?**

* **Explanation:** Optimistic concurrency control assumes no conflicts during execution and validates changes at the end, while pessimistic concurrency control locks resources from the start and prevents concurrent access.

#### 24. **Explain the role of `std::packaged_task` in C++ and provide an example.**

*   **Code:**

    ```cpp
    #include <iostream>
    #include <future>

    int add(int a, int b) {
        return a + b;
    }

    int main() {
        std::packaged_task<int(int, int)> task(add);
        std::future<int> result = task.get_future();

        std::thread t(std::move(task), 3, 4);
        t.join();

        std::cout << "Result: " << result.get() << std::endl;

        return 0;
    }
    ```
* **Explanation:** `std::packaged_task` is a wrapper for a callable object, allowing it to be executed asynchronously and obtaining its result through a `std::future`.

#### 25. **What is the role of memory barriers in concurrent programming?**

* **Explanation:** Memory barriers ensure that memory operations are completed in a specified order, preventing reordering by the compiler or hardware. They are crucial for maintaining the correctness of concurrent code.

#### 26. **How does the C++ memory model ensure consistency in multithreaded programs?**

* **Explanation:** The C++ memory model defines rules for the visibility and ordering of memory operations between threads, ensuring consistency in multithreaded programs.

#### 27. **Explain the concept of lock-free programming in C++.**

*   **Code:**

    ```cpp
    #include <iostream>
    #include <atomic>
    #include <thread>

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
* **Explanation:** Lock-free programming aims to design algorithms and data structures that can be safely used by multiple threads without the need for locks, ensuring progress even in the presence of contention.

#### 28. **What is a condition variable timeout, and how can it be implemented?**

*   **Code:**

    ```cpp
    #include <iostream>
    #include <thread>
    #include <mutex>
    #include <condition_variable>
    #include <chrono>

    std::mutex mtx;
    std::condition_variable cv;
    bool dataReady = false;

    void waitForData() {
        std::unique_lock<std::mutex> lock(mtx);
        if (cv.wait_for(lock, std::chrono::milliseconds(500), [] { return dataReady; })) {
            std::cout << "Data is ready!" << std::endl;
        } else {
            std::cout << "Timeout occurred!" << std::endl;
        }
    }

    void provideData() {
        std::this_thread::sleep_for(std::chrono::milliseconds(1000));
        {
            std::lock_guard<std::mutex> lock(mtx);
            dataReady = true;
        }
        cv.notify_one();
    }

    int main() {
        std::thread t1(waitForData);
        std::thread t2(provideData);

        t1.join();
        t2.join();

        return 0;
    }
    ```
* **Explanation:** This question checks the understanding of condition variable timeouts, allowing a thread to wait for a condition for a specified duration and handling the case when the condition is not met within the timeout.

#### 29. **What is the role of `std::promise` and `std::future` in C++ concurrency?**

*   **Code:**

    ```cpp
    #include <iostream>
    #include <thread>
    #include <future>

    void worker(std::promise<int>& p) {
        // Perform some work
        int result = 42;
        p.set_value(result);
    }

    int main() {
        std::promise<int> promise;
        std::future<int> result = promise.get_future();

        std::thread t(worker, std::ref(promise));
        t.join();

        std::cout << "Result: " << result.get() << std::endl;

        return 0;
    }
    ```
* **Explanation:** `std::promise` is used to communicate a value or an exception from one thread to another, and `std::future` is used to retrieve the result or exception asynchronously.

#### 30. **Explain the concept of transactional memory in C++ and its advantages.**

* **Explanation:** Transactional memory allows multiple threads to execute code in a transaction, ensuring atomicity and isolation. It simplifies concurrent programming by automatically handling locks and providing rollback in case of conflicts.
