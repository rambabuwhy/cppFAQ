# Basics - 1

#### 1. **What is the difference between C and C++?**

**Answer:** C++ is an extension of C with the addition of object-oriented features. It supports classes and objects, encapsulation, inheritance, and polymorphism, which are not present in C.

#### 2. **Explain the difference between `new` and `malloc` in C++.**

**Answer:** `new` is an operator in C++ for dynamic memory allocation, while `malloc` is a function in C. `new` calls the constructor for the allocated memory, and `malloc` doesn't. `new` returns a pointer to the allocated memory with the specified type, ensuring type safety.

#### 3. **What is the difference between reference and a pointer?**

**Answer:** Both reference and pointer provide a way to refer to another object indirectly. However, key differences include:

* References cannot be null and must be initialized at the time of declaration.
* Pointers can be reassigned and can point to null.
* References use the same syntax as the original variable.

#### 4. **What is the difference between `delete` and `delete[]`?**

**Answer:** `delete` is used to deallocate memory allocated using `new`, while `delete[]` is used for memory allocated with `new[]`. Using the wrong one can lead to undefined behavior.

#### 5. **Explain what the "const" keyword means in C++.**

**Answer:** `const` is used to declare constants and indicate that a variable's value cannot be modified. It can be applied to variables, function parameters, and member functions.

#### 6. **What is a virtual function?**

**Answer:** A virtual function in C++ is a function in a base class that is declared with the `virtual` keyword and can be overridden by a function with the same signature in a derived class. It enables polymorphism.

#### 7. **What is the difference between shallow copy and deep copy?**

**Answer:** Shallow copy duplicates the memory addresses of the original object's members, whereas deep copy duplicates the content of the members, creating new memory locations.

#### 8. **Explain the "Rule of Three" in C++.**

**Answer:** The Rule of Three states that if a class defines one of the following three special member functions, it should define all three:

* Destructor
* Copy constructor
* Copy assignment operator

#### 9. **What is the purpose of the `explicit` keyword?**

**Answer:** The `explicit` keyword is used to prevent implicit type conversions in C++. It is often used with single-argument constructors to avoid unintended type conversions.

#### 10. **Explain the concept of a template in C++.**

**Answer:** Templates in C++ allow the creation of generic classes or functions that can work with different data types without specifying the data type in advance. They provide a way to write flexible and reusable code.
