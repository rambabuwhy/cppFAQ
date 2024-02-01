# Thread-7

#### Problem 11: Task Execution Framework

**Problem:** Implement a simple task execution framework in C++. The framework should allow submitting tasks that are executed by a pool of worker threads. Additionally, tasks should support dependencies, ensuring that a task is only executed when its dependencies have been completed.

**Code:**

```cpp
#include <iostream>
#include <vector>
#include <thread>
#include <mutex>
#include <condition_variable>
#include <functional>
#include <queue>

class Task {
public:
    virtual void execute() = 0;
    virtual ~Task() = default;
};

class SimpleTask : public Task {
private:
    std::function<void()> task;

public:
    explicit SimpleTask(std::function<void()> t) : task(std::move(t)) {}

    void execute() override {
        task();
    }
};

class TaskFramework {
private:
    std::vector<std::thread> workers;
    std::queue<Task*> taskQueue;
    std::mutex queueMutex;
    std::condition_variable queueNotEmpty;

    bool stop;

public:
    TaskFramework(size_t numThreads) : stop(false) {
        for (size_t i = 0; i < numThreads; ++i) {
            workers.emplace_back([this] { workerThread(); });
        }
    }

    ~TaskFramework() {
        {
            std::unique_lock<std::mutex> lock(queueMutex);
            stop = true;
        }
        queueNotEmpty.notify_all();

        for (std::thread& worker : workers) {
            worker.join();
        }

        while (!taskQueue.empty()) {
            delete taskQueue.front();
            taskQueue.pop();
        }
    }

    void submitTask(Task* task) {
        {
            std::unique_lock<std::mutex> lock(queueMutex);
            taskQueue.push(task);
        }
        queueNotEmpty.notify_one();
    }

    void submitDependencyTask(Task* task, Task* dependency) {
        dependency->execute();
        submitTask(task);
    }

private:
    void workerThread() {
        while (true) {
            std::unique_lock<std::mutex> lock(queueMutex);

            queueNotEmpty.wait(lock, [this] { return stop || !taskQueue.empty(); });

            if (stop && taskQueue.empty()) {
                return;
            }

            Task* currentTask = taskQueue.front();
            taskQueue.pop();

            lock.unlock();

            currentTask->execute();
            delete currentTask;
        }
    }
};

void simpleTaskFunction(int id) {
    std::cout << "Simple task executed by thread " << id << std::endl;
}

void dependentTaskFunction(int id) {
    std::cout << "Dependent task executed by thread " << id << std::endl;
}

int main() {
    TaskFramework taskFramework(3);

    SimpleTask* simpleTask = new SimpleTask([&] { simpleTaskFunction(1); });
    taskFramework.submitTask(simpleTask);

    SimpleTask* dependentTask = new SimpleTask([&] { dependentTaskFunction(2); });
    SimpleTask* dependentTask2 = new SimpleTask([&] { dependentTaskFunction(3); });

    taskFramework.submitDependencyTask(dependentTask, simpleTask);
    taskFramework.submitDependencyTask(dependentTask2, simpleTask);

    return 0;
}
```

**Explanation:** This problem assesses the candidate's understanding of task execution frameworks and task dependencies. The `TaskFramework` class manages a pool of worker threads that execute submitted tasks. Dependencies are handled by ensuring that a task is executed only when its dependencies have completed.

***

#### Problem 12: Thread-Local Storage

**Problem:** Use thread-local storage to implement a simple thread-safe counter in C++. Each thread should have its own counter that increments independently.

**Code:**

```cpp
#include <iostream>
#include <thread>
#include <mutex>
#include <vector>
#include <thread>

thread_local int threadCounter = 0;
std::mutex globalCounterMutex;

void incrementCounter() {
    std::lock_guard<std::mutex> lock(globalCounterMutex);
    threadCounter++;
    std::cout << "Thread " << std::this_thread::get_id() << ": Counter = " << threadCounter << std::endl;
}

int main() {
    std::vector<std::thread> threads;

    for (int i = 0; i < 5; ++i) {
        threads.emplace_back(incrementCounter);
    }

    for (auto& thread : threads) {
        thread.join();
    }

    return 0;
}
```

**Explanation:** This problem tests the candidate's understanding of thread-local storage. The `thread_local` keyword is used to declare a variable that has a separate instance for each thread. In this example, each thread increments its own counter independently.

***

#### Problem 13: ABA Problem with CAS

**Problem:** Implement a solution to the ABA problem using Compare-And-Swap (CAS) in C++. Simulate a scenario where the ABA problem can occur and demonstrate its resolution.

**Code:**

```cpp
#include <iostream>
#include <atomic>
#include <thread>

std::atomic<int> sharedValue(1);

void worker1() {
    int expected = 1;
    int new_value = 2;
    
    if (sharedValue.compare_exchange_strong(expected, new_value)) {
        std::cout << "Worker 1: Value changed successfully." << std::endl;
    }

    std::this_thread::sleep_for(std::chrono::milliseconds(100));

    expected = 2;
    new_value = 3;

    if (sharedValue.compare_exchange_strong(expected, new_value)) {
        std::cout << "Worker 1: Value changed successfully." << std::endl;
    }
}

void worker2() {
    int value = sharedValue.load();

    std::this_thread::sleep_for(std::chrono::milliseconds(50));

    if (sharedValue.compare_exchange_strong(value, 1)) {
        std::cout << "Worker 2: Value changed successfully." << std::endl;
    } else {
        std::cout << "Worker 2: Value change failed." << std::endl;
    }
}

int main() {
    std::thread t1(worker1);
    std::thread t2(worker2);

    t1.join();
    t2.join();

    return 0;
}
```

**Explanation:** This problem assesses the candidate's understanding of the ABA problem and how to solve it using the Compare-And-Swap (CAS) operation. The workers simulate a scenario where the ABA problem can occur, and CAS is used to address it.

***

#### Problem 14: Thread-Safe Singleton

**Problem:** Implement a thread-safe singleton class in C++ using double-checked locking. Ensure that only a single instance of the class is created.

**Code:**

```cpp
#include <iostream>
#include <mutex>

class ThreadSafeSingleton {
private:
    static ThreadSafeSingleton* instance;
    static std::mutex creationMutex;

    ThreadSafeSingleton() {}

public:
    static ThreadSafeSingleton* getInstance() {
        if (instance == nullptr) {
            std::lock_guard<std::mutex> lock(creationMutex);
            if (instance == nullptr) {
                instance = new ThreadSafeSingleton();
            }
        }
        return instance;
    }
};

ThreadSafeSingleton* ThreadSafeSingleton::instance = nullptr;
std::mutex ThreadSafeSingleton::creationMutex;

int main() {
    ThreadSafeSingleton* obj1 = ThreadSafeSingleton::getInstance();
    ThreadSafeSingleton* obj2 = ThreadSafeSingleton::getInstance();

    std::cout << "obj1 address: " << obj1 << std::endl;
    std::cout << "obj2 address: " << obj2 << std::endl;

    return 0;
}
```

**Explanation:** This problem assesses the candidate's understanding of implementing a thread-safe singleton class using double-checked locking. The `ThreadSafeSingleton` class ensures that only one instance is created, and the `getInstance` method provides a thread-safe way to access it.

***

#### Problem 15: Task Ordering

**Problem:** Implement a program in C++ where multiple tasks need to be executed in a specific order. Use thread synchronization mechanisms to ensure that the tasks are executed in the correct sequence.

**Code:**

```cpp
#include <iostream>
#include <thread>
#include <mutex>

std::mutex mutex1, mutex2;

void task1() {
    std::unique_lock<std::mutex> lock(mutex1);
    std::cout << "Task 1 executed." << std::endl;
}

void task2() {
    std::unique_lock<std::mutex> lock(mutex2);
    std::cout << "Task 2 executed." << std::endl;
}

void task3() {
    std::unique_lock<std::mutex> lock(mutex1);
    std::cout << "Task 3 executed." << std::endl;
}

void task4() {
    std::unique_lock<std::mutex> lock(mutex2);
    std::cout << "Task 4 executed." << std::endl;
}

int main() {
    std::thread t1(task1);
    std::thread t2(task2);
    std::thread t3(task3);
    std::thread t4(task4);

    t1.join();
    t2.join();
    t3.join();
    t4.join();

    return 0;
}
```

**Explanation:** This problem assesses the candidate's ability to synchronize tasks in a specific order using thread synchronization mechanisms. The tasks are executed in a predefined sequence using two mutexes (`mutex1` and `mutex2`) to control the order.
