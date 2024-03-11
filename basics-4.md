# Basics - 6

#### 31. **Explain the difference between `std::thread` and `std::async` in C++.**

**Answer:** `std::thread` is used for creating and managing threads in a more manual way, while `std::async` is a higher-level abstraction that allows for asynchronous execution and provides a future to retrieve the result.

#### 32. **What is the Rule of Five in C++?**

**Answer:** The Rule of Five states that if a class defines one of the following special member functions, it should define all five:

* Destructor
* Copy constructor
* Move constructor
* Copy assignment operator
* Move assignment operator

#### 33. **What is the purpose of the `constexpr` specifier in C++?**

**Answer:** The `constexpr` specifier is used to indicate that a variable or function can be evaluated at compile time. It allows for performance improvements by enabling constant expressions.

#### 34. **Explain the concept of move semantics in C++.**

**Answer:** Move semantics in C++ allow the efficient transfer of resources (like memory ownership) from one object to another. It is implemented using move constructors and move assignment operators.

#### 35. **What are pure virtual functions, and when are they used?**

**Answer:** Pure virtual functions are declared with `= 0` in a base class and have no implementation. They make the class abstract and must be overridden by derived classes. They are used to achieve polymorphism and create abstract base classes.

#### 36. **How does the `std::unique_lock` differ from `std::lock_guard`?**

**Answer:** Both are used for managing locks, but `std::unique_lock` provides more flexibility. It can be unlocked and re-locked, and it supports deferred locking and timed locking, while `std::lock_guard` is simpler and more lightweight.

#### 37. **What is the role of the `explicit` keyword with a single-argument constructor?**

**Answer:** The `explicit` keyword in a single-argument constructor prevents implicit type conversions. It ensures that the constructor is only used for explicit type conversions and not for implicit conversions.

#### 38. **Explain the purpose of the `std::forward` function in C++11 and later.**

**Answer:** `std::forward` is used to perfectly forward arguments in C++11 and later. It preserves the value category (lvalue or rvalue) of its argument when passed to another function, especially useful in template metaprogramming.

#### 39. **What are the differences between a `struct` and a `class` in C++?**

**Answer:** In C++, `struct` and `class` are almost identical, with the only difference being the default access level. Members of a `struct` are public by default, while members of a `class` are private by default.

#### 40. **Explain the role of the `std::initializer_list` in C++.**

**Answer:** `std::initializer_list` is a feature introduced in C++11 to enable uniform initialization of objects using curly braces `{}`. It is often used in constructor overloads to accept a variable number of arguments.
