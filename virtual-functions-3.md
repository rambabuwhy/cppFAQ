# Virtual Functions - 3

#### 21. What is the purpose of the `virtual` keyword in a derived class that overrides a virtual function?

**Answer:** While it is not mandatory, using the `virtual` keyword in a derived class that overrides a virtual function helps in making the code more readable and explicit. It reminds the developer that the function is intended to override a virtual function from the base class.

```cpp
class Base {
public:
    virtual void myVirtualFunction() {
        // Base class implementation
    }
};

class Derived : public Base {
public:
    virtual void myVirtualFunction() override {
        // Derived class implementation
    }
};
```

#### 22. Explain the concept of multiple inheritance and its impact on virtual functions.

**Answer:** Multiple inheritance occurs when a class is derived from more than one base class. In the context of virtual functions, multiple inheritance can lead to the diamond problem. C++ provides virtual inheritance to address this issue and ensure that only one instance of a common base class exists in the hierarchy.

#### 23. What is the difference between early binding and late binding in the context of function calls?

**Answer:** Early binding (static binding) refers to the resolution of function calls at compile-time, based on the declared type of the object. Late binding (dynamic binding) involves resolving function calls at runtime, taking into account the actual type of the object, typically associated with virtual functions and polymorphism.

#### 24. How does the `typeid` operator differ from the `dynamic_cast` operator in C++?

**Answer:** The `typeid` operator is used to obtain type information at runtime and returns a `std::type_info` object. On the other hand, the `dynamic_cast` operator is used for safe downcasting in polymorphic class hierarchies and returns a pointer or reference to the derived type if the conversion is valid, otherwise, it returns `nullptr` or throws an exception.

#### 25. Can a non-member function be virtual in C++?

**Answer:** No, virtual functions are associated with class instances, and non-member functions do not belong to any specific class. Therefore, only member functions of classes (including friend functions) can be declared as virtual.

#### 26. What is the purpose of the `final` keyword when used with a class?

**Answer:** The `final` keyword when used with a class indicates that the class cannot be further derived. It helps in enforcing design decisions and preventing unintentional modification of the inheritance hierarchy beyond the specified class.

#### 27. How does the order of declaration of virtual functions impact the vtable?

**Answer:** The order of declaration of virtual functions in a class does not impact the vtable. The vtable is created based on the order of the virtual functions' declarations in the base class and is inherited by derived classes.

#### 28. Can a destructor be pure virtual in C++?

**Answer:** Yes, a destructor can be pure virtual in C++. This makes the class abstract, and any derived class must provide its implementation for the destructor. However, it is less common to have a pure virtual destructor.

```cpp
class AbstractBase {
public:
    virtual ~AbstractBase() = 0;
};

AbstractBase::~AbstractBase() {
    // Pure virtual destructor requires a definition
}
```

#### 29. Explain the concept of slicing in C++.

**Answer:** Slicing occurs when an object of a derived class is assigned to an object of a base class, resulting in the loss of the derived class-specific information. This happens if the assignment is done by value and not by reference or pointer.

```cpp
class Base {
public:
    int data;
};

class Derived : public Base {
public:
    int derivedData;
};

// Slicing example
Derived derivedObj;
Base baseObj = derivedObj;  // Slicing occurs, derivedData is lost
```

#### 30. How does the `sizeof` operator behave in the presence of virtual functions?

**Answer:** The `sizeof` operator includes the size of any non-static data members of the class and additional space for virtual functions. Each object of a class with virtual functions typically contains a pointer to the vtable, which contributes to the size of the object. The exact size may vary depending on the compiler and platform.
