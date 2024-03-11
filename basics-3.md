# Basics - 5

#### 21. **What is the difference between `delete` and `delete[]` when freeing memory?**

**Answer:** `delete` is used to deallocate memory for a single object allocated with `new`, while `delete[]` is used to deallocate memory for an array of objects allocated with `new[]`. Using the wrong one can lead to undefined behavior.

#### 22. **Explain the role of the `const_iterator` in C++ standard containers.**

**Answer:** `const_iterator` is an iterator that allows read-only access to the elements of a C++ standard container. It is used when iterating over a container without modifying its elements.

#### 23. **What is the purpose of the `friend` keyword in C++?**

**Answer:** The `friend` keyword is used to grant non-member functions or other classes access to private or protected members of a class. It is often used to allow specific functions or classes to access internal details without violating encapsulation.

#### 24. **Explain the difference between shallow copy and deep copy in the context of copy constructors.**

**Answer:** A shallow copy in a copy constructor copies the memory addresses of the original object's members, while a deep copy creates new memory locations and copies the content of the members.

#### 25. **What is the significance of the `volatile` keyword in C++?**

**Answer:** The `volatile` keyword is used to indicate that a variable may be changed at any time by external factors, such as hardware. It prevents the compiler from optimizing away reads or writes to the variable.

#### 26. **How does exception handling work in C++?**

**Answer:** C++ uses the `try`, `catch`, and `throw` keywords for exception handling. Code that might throw an exception is placed in a `try` block, and the corresponding exception is caught in a `catch` block. Exceptions are thrown using the `throw` keyword.

#### 27. **What is the purpose of the `std::move` constructor in C++?**

**Answer:** The `std::move` constructor is used to explicitly convert an object into an rvalue, enabling move semantics. It is often used to efficiently transfer ownership or resources between objects.

#### 28. **Explain the difference between stack and heap memory in C++.**

**Answer:** Stack memory is used for local variables and function call management, while heap memory is dynamically allocated and deallocated during runtime. Stack memory is faster but limited in size, while heap memory provides more flexibility.

#### 29. **What is the purpose of the `explicit` specifier in C++?**

**Answer:** The `explicit` specifier is used to prevent implicit type conversions by constructors. It ensures that a constructor is only used for explicit type conversions and not for implicit conversions.

#### 30. **What is a lambda expression in C++?**

**Answer:** A lambda expression is an anonymous function defined using the `[]` syntax. It allows the creation of functions locally and is often used in conjunction with algorithms or functional programming constructs.
