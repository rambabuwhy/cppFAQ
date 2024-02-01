# Smart pointer-2

#### Question 6:

**Explain custom deleters in smart pointers. Provide an example.**

**Answer:** Custom deleters allow you to define a specific way to release the memory associated with a smart pointer. This can be useful when dealing with resources other than heap-allocated memory.

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
    std::unique_ptr<int, CustomDeleter> uniquePtr(new int(42));
    // When uniquePtr goes out of scope, the custom deleter is called.
    return 0;
}
```

#### Question 7:

**Discuss the use of `std::make_shared` and `std::make_unique` and their advantages over using `new`.**

**Answer:** `std::make_shared` and `std::make_unique` are helper functions that create smart pointers with better performance and exception safety compared to using `new` directly.

```cpp
#include <memory>

int main() {
    // Using make_shared
    auto sharedPtr = std::make_shared<int>(42);

    // Using make_unique (C++14 and later)
    auto uniquePtr = std::make_unique<int>(42);
    
    // Both functions allocate and initialize the object in a single step, reducing overhead.
    return 0;
}
```

#### Question 8:

**Explain the role of `std::enable_shared_from_this` and provide an example.**

**Answer:** `std::enable_shared_from_this` is a mixin class template that provides the `shared_from_this` member function, allowing a class to create a `shared_ptr` from within a member function.

```cpp
#include <memory>

class MyClass : public std::enable_shared_from_this<MyClass> {
public:
    std::shared_ptr<MyClass> getShared() {
        return shared_from_this();
    }
};

int main() {
    std::shared_ptr<MyClass> obj = std::make_shared<MyClass>();
    std::shared_ptr<MyClass> sharedObj = obj->getShared();
    // sharedObj and obj share ownership of the same object.
    return 0;
}
```

#### Question 9:

**Discuss the potential pitfalls and misuse of smart pointers.**

**Answer:** Smart pointers are powerful but can be misused. Common pitfalls include circular dependencies, using `std::shared_ptr` when `std::unique_ptr` is sufficient, and improper use of `std::weak_ptr`. Understanding ownership and lifetimes is crucial to avoiding pitfalls.

#### Question 10:

**How does move semantics relate to smart pointers? Provide an example.**

**Answer:** Move semantics allow the efficient transfer of ownership between smart pointers, reducing unnecessary copying of resources.

```cpp
#include <memory>

int main() {
    std::unique_ptr<int> sourcePtr = std::make_unique<int>(42);
    std::unique_ptr<int> destinationPtr = std::move(sourcePtr);
    // Ownership transferred efficiently without deep copying.
    return 0;
}
```

These a
