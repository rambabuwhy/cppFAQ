# Thread -1

#### 1. **What is a Thread?**

*   **Code:**

    ```cpp
    #include <iostream>
    #include <thread>

    void threadFunction() {
        std::cout << "Hello from thread!" << std::endl;
    }

    int main() {
        std::thread t(threadFunction);
        t.join();
        return 0;
    }
    ```
* **Explanation:** This question tests the candidate's understanding of basic threading concepts. A thread is a lightweight process, and in C++, you can create and manage threads using the `<thread>` header.

#### 2. **What is the difference between a thread and a process?**

* **Explanation:** This question assesses the candidate's knowledge of basic operating system concepts. A process has its own memory space, while threads within a process share the same memory space.

#### 3. **What is a race condition, and how can you prevent it in C++?**

*   **Code:**

    ```cpp
    #include <iostream>
    #include <thread>
    #include <mutex>

    int counter = 0;
    std::mutex mtx;

    void increment() {
        for (int i = 0; i < 100000; ++i) {
            std::lock_guard<std::mutex> lock(mtx);
            counter++;
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
* **Explanation:** This question checks if the candidate understands race conditions and how to prevent them using mutexes. In the example, `std::lock_guard` is used to ensure exclusive access to the shared resource (`counter`).

#### 4. **What is deadlock, and how can it be avoided?**

* **Explanation:** Deadlock occurs when two or more threads wait indefinitely for each other to release resources. Avoiding deadlock involves careful resource allocation and avoiding circular wait.

#### 5. **Explain the concept of thread safety.**

* **Explanation:** Thread safety ensures that a piece of code can be safely executed by multiple threads concurrently without causing data corruption or unexpected behavior. Techniques like mutexes, atomic operations, and locks are used to achieve thread safety.

#### 6. **What is std::async in C++?**

*   **Code:**

    ```cpp
    #include <iostream>
    #include <future>

    int foo() {
        return 42;
    }

    int main() {
        std::future<int> result = std::async(foo);
        std::cout << "Result: " << result.get() << std::endl;
        return 0;
    }
    ```
* **Explanation:** `std::async` is used for asynchronous task execution. It returns a `std::future` representing the result of the asynchronous operation.

#### 7. **Explain condition variables and their usage in C++.**

*   **Code:**

    ```cpp
    #include <iostream>
    #include <thread>
    #include <mutex>
    #include <condition_variable>

    std::mutex mtx;
    std::condition_variable cv;
    bool ready = false;

    void worker() {
        std::unique_lock<std::mutex> lock(mtx);
        cv.wait(lock, [] { return ready; });
        std::cout << "Worker thread is working!" << std::endl;
    }

    int main() {
        std::thread t(worker);

        {
            std::lock_guard<std::mutex> lock(mtx);
            ready = true;
        }

        cv.notify_one();
        t.join();

        return 0;
    }
    ```
* **Explanation:** Condition variables are used for communication between threads. They allow one thread to signal another when a condition is met.

#### 8. **What is the purpose of std::atomic in C++?**

*   **Code:**

    ```cpp
    #include <iostream>
    #include <thread>
    #include <atomic>

    std::atomic<int> counter(0);

    void increment() {
        for (int i = 0; i < 100000; ++i) {
            counter++;
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
* **Explanation:** `std::atomic` provides atomic operations, ensuring that operations on the variable are executed atomically without the need for locks.

#### 9. **Explain the concept of a condition variable and how it differs from a mutex.**

* **Explanation:** A condition variable is used for communication between threads, allowing one thread to signal another when a condition is met. It differs from a mutex in that it doesn't provide exclusive access to a resource but rather signals the state of a shared resource.

#### 10. **What is a thread pool, and why might it be useful?**

* **Explanation:** A thread pool is a collection of worker threads that are created once and reused to execute tasks. It is useful for reducing the overhead of thread creation and managing the number of concurrently executing tasks.
