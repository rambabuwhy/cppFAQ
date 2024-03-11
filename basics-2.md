# Basics - 3

#### 11. **What is a smart pointer in C++?**

**Answer:** A smart pointer in C++ is an object that acts like a pointer but provides additional functionalities, such as automatic memory management. Examples include `std::unique_ptr` and `std::shared_ptr`.

#### 12. **Explain the difference between `const` and `constexpr` in C++.**

**Answer:** `const` is used to indicate that a variable's value cannot be modified, while `constexpr` is used to specify that a variable or function can be evaluated at compile time.

#### 13. **What is an inline function?**

**Answer:** An inline function is a function that the compiler may choose to expand at the point of the function call, rather than performing a regular function call. It is a suggestion to the compiler and can improve performance for small functions.

#### 14. **What is the purpose of the `mutable` keyword in C++?**

**Answer:** The `mutable` keyword is used to indicate that a particular data member of a `const` object can be modified. It is often used with `mutable` members in classes.

#### 15. **Explain the concept of RAII (Resource Acquisition Is Initialization) in C++.**

**Answer:** RAII is a programming technique where resource management (like memory allocation) is tied to object lifetime. Resources are acquired in the constructor and released in the destructor.

#### 16. **What is the difference between `override` and `final` specifiers in C++?**

**Answer:** The `override` specifier is used to indicate that a function is intended to override a virtual function, while `final` is used to indicate that a virtual function cannot be overridden further in derived classes.

#### 17. **What is the purpose of the `std::move` function?**

**Answer:** `std::move` is used to convert an lvalue into an rvalue, enabling the efficient transfer of ownership or resources. It is often used with move semantics in C++11 and later.

#### 18. **What are the differences between `std::vector` and `std::array`?**

**Answer:** `std::vector` is a dynamic array that can change in size, while `std::array` is a fixed-size array with a static size specified at compile time. `std::vector` is more flexible but may incur dynamic memory allocation overhead.

#### 19. **Explain the purpose of the `explicit` keyword in a constructor.**

**Answer:** The `explicit` keyword in a constructor prevents implicit type conversions during object construction. It ensures that the constructor is only used for explicit type conversions.

#### 20. **What is the role of the `typeid` operator in C++?**

**Answer:** The `typeid` operator is used to obtain information about the type of an expression or an object at runtime. It returns a `std::type_info` object, which can be used for type checking and dynamic type identification.
