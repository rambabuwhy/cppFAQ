# Virtual Functions - 1

#### 1. What is a virtual function in C++?

**Answer:** In C++, a virtual function is a member function declared within a base class that is intended to be overridden by derived classes. It allows dynamic polymorphism by enabling late binding, where the appropriate function is determined at runtime.

#### 2. How is a virtual function declared?

**Answer:** To declare a function as virtual in C++, you use the `virtual` keyword in the base class declaration. For example:

```cpp
class Base {
public:
    virtual void myVirtualFunction() {
        // Implementation
    }
};
```

#### 3. What is the significance of the `virtual` keyword?

**Answer:** The `virtual` keyword signifies that a function can be overridden by derived classes, enabling polymorphic behavior. It is essential for achieving dynamic binding during runtime.

#### 4. Can a virtual function have a body in the base class?

**Answer:** Yes, a virtual function can have a body in the base class. However, it is not mandatory. The presence of a body in the base class allows it to provide a default implementation, which can be overridden by derived classes.

#### 5. What is pure virtual function?

**Answer:** A pure virtual function is a virtual function declared in a base class with no implementation in the base class. It is denoted by appending `= 0` to the function declaration. Classes containing pure virtual functions are abstract, and they cannot be instantiated.

```cpp
class AbstractBase {
public:
    virtual void pureVirtualFunction() = 0;
};
```

#### 6. Can you override a non-virtual function in C++?

**Answer:** No, non-virtual functions do not support polymorphism through late binding. They are statically bound, and the function called is determined at compile-time. Therefore, overriding is not applicable to non-virtual functions.

#### 7. What is the difference between function overloading and function overriding?

**Answer:** Function overloading involves defining multiple functions in the same scope with the same name but different parameter lists. Function overriding, on the other hand, occurs in the context of inheritance when a derived class provides a specific implementation for a virtual function declared in the base class.

#### 8. Can a constructor be virtual in C++?

**Answer:** No, constructors cannot be virtual in C++. Virtual functions are used for dynamic polymorphism, but constructors are called during object creation, and the determination of which constructor to call is based on the static type of the object.

#### 9. Explain the concept of vtable (Virtual Table) in C++.

**Answer:** The vtable is a table of function pointers maintained by the compiler for classes that have virtual functions. Each class with virtual functions has a vtable that holds pointers to the virtual functions. During runtime, the correct function to call is determined by looking up the vtable associated with the object's type.

#### 10. What is the "virtual destructor" in C++ and why is it necessary?

**Answer:** A virtual destructor is a destructor declared with the `virtual` keyword in the base class. It is essential when dealing with polymorphic objects to ensure that the appropriate destructor is called for the derived class when deleting a base class pointer. This helps prevent memory leaks and ensures proper cleanup in the presence of inheritance.

\
