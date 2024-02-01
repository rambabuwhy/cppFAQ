# Smart pointer-1

#### Question 1:

**What is a smart pointer? Can you name some smart pointers provided by C++?**

**Answer:** A smart pointer is an object that acts like a pointer but provides additional features, such as automatic memory management. C++ provides three types of smart pointers: `std::unique_ptr`, `std::shared_ptr`, and `std::weak_ptr`.

#### Question 2:

**Explain `std::unique_ptr`. Provide an example of its usage.**

**Answer:** `std::unique_ptr` is a smart pointer that owns and manages a dynamically allocated object. It ensures that there is only one `std::unique_ptr` pointing to a particular resource.

```cpp
#include <memory>

int main() {
    std::unique_ptr<int> uniquePtr = std::make_unique<int>(42);
    // uniquePtr owns the dynamically allocated integer
    // When uniquePtr goes out of scope, the memory is automatically deallocated.
    return 0;
}
```

#### Question 3:

**What is the purpose of `std::shared_ptr`? Provide an example.**

**Answer:** `std::shared_ptr` is a smart pointer that allows multiple `shared_ptr` instances to share ownership of the same dynamically allocated object. It keeps a reference count, and the memory is deallocated when the last `shared_ptr` pointing to the object is destroyed.

```cpp
#include <memory>

int main() {
    std::shared_ptr<int> sharedPtr1 = std::make_shared<int>(42);
    std::shared_ptr<int> sharedPtr2 = sharedPtr1; // Both shared pointers share ownership
    // When both shared pointers are out of scope, memory is deallocated.
    return 0;
}
```

#### Question 4:

**Explain the concept of `std::weak_ptr`. Provide a use case.**

**Answer:** `std::weak_ptr` is a smart pointer that does not contribute to the reference count of the managed object. It is often used in conjunction with `std::shared_ptr` to break circular references.

```cpp
#include <memory>

int main() {
    std::shared_ptr<int> sharedPtr = std::make_shared<int>(42);
    std::weak_ptr<int> weakPtr = sharedPtr; // weakPtr doesn't affect the reference count
    // Use weakPtr when strong ownership is not required, preventing circular references.
    return 0;
}
```

#### Question 5:

**What are the benefits of using smart pointers over raw pointers?**

**Answer:** Smart pointers provide automatic memory management, reducing the chances of memory leaks and simplifying memory handling. They offer better safety and exception safety compared to raw pointers, making code more robust and less error-prone.
