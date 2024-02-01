# Smart pointer-4

#### Problem 1:

**Memory Management and Ownership**

Write a function that takes a raw pointer to an array of integers and returns a `std::unique_ptr` that owns the array. Ensure proper memory management and avoid memory leaks.

```cpp
#include <memory>

std::unique_ptr<int[]> createIntArray(int size) {
    // Your implementation here
}

int main() {
    std::unique_ptr<int[]> arrayPtr = createIntArray(5);
    // Use the arrayPtr as needed
    return 0;
}
```

#### Problem 2:

**Circular References**

Create a class structure that involves circular references using `std::shared_ptr` and `std::weak_ptr`. Implement a mechanism to break the circular references and avoid memory leaks.

```cpp
#include <memory>

class Node;

class Edge {
public:
    std::shared_ptr<Node> connectedNode;
};

class Node {
public:
    std::shared_ptr<Edge> outgoingEdge;
    std::weak_ptr<Edge> incomingEdge;
};

int main() {
    // Create a circular reference and break it
    // Your implementation here
    return 0;
}
```

#### Problem 3:

**Custom Deleter**

Implement a custom deleter for a `std::shared_ptr` that logs a message when the shared object is deleted. Use this custom deleter in a shared pointer and demonstrate its usage.

```cpp
#include <memory>
#include <iostream>

struct CustomDeleter {
    void operator()(int* p) const {
        std::cout << "Custom Deleter Called\n";
        delete p;
    }
};

int main() {
    // Use std::shared_ptr with the custom deleter
    // Your implementation here
    return 0;
}
```

#### Problem 4:

**Converting Raw Pointers**

Write a function that takes a raw pointer and converts it into a `std::shared_ptr` and a `std::unique_ptr`. Discuss the differences between the two smart pointers in this context.

```cpp
#include <memory>

void convertRawPointer(int* rawPtr) {
    // Your implementation here
}

int main() {
    int* rawPtr = new int(42);
    convertRawPointer(rawPtr);
    // Ensure proper memory management
    return 0;
}
```

#### Problem 5:

**Thread Safety with Shared Pointers**

Write a multithreaded program where multiple threads share a `std::shared_ptr` to a resource. Implement proper synchronization mechanisms to ensure thread safety and prevent data races.

```cpp
#include <memory>
#include <iostream>
#include <thread>
#include <vector>

class SharedResource {
public:
    int data;
    // Add necessary synchronization mechanisms
};

void threadFunction(std::shared_ptr<SharedResource> sharedPtr) {
    // Your implementation here
}

int main() {
    std::shared_ptr<SharedResource> sharedPtr = std::make_shared<SharedResource>();

    // Create multiple threads that access the sharedPtr concurrently
    // Your implementation here

    return 0;
}
```

These interview problems cover various aspects of smart pointers, including memory management, circular references, custom deleters, converting raw pointers, and thread safety. They are designed to test a candidate's practical understanding of smart pointer concepts and their application in real-world scenarios.
