# Virtual Functions - 2

11\. Can a virtual function be static in C++?

**Answer:** No, virtual functions cannot be static. The `static` keyword is incompatible with the concept of virtual functions because static functions are resolved at compile-time, whereas virtual functions are resolved at runtime.

#### 12. What is the purpose of the `override` specifier in C++?

**Answer:** The `override` specifier is used in derived class declarations to explicitly indicate that a function is intended to override a virtual function from a base class. It enhances code readability and helps catch errors during compilation if the specified function doesn't actually override a base class function.

```cpp
class Derived : public Base {
public:
    void myVirtualFunction() override {
        // Implementation in the derived class
    }
};
```

#### 13. Explain the difference between early binding and late binding.

**Answer:** Early binding (static binding) occurs at compile-time and involves resolving function calls based on the declared type of the object. Late binding (dynamic binding) occurs at runtime and is associated with polymorphism, where the appropriate function implementation is determined based on the actual type of the object.

#### 14. What is the "diamond problem" in C++ and how does virtual inheritance address it?

**Answer:** The diamond problem arises in multiple inheritance when a class inherits from two classes that both inherit from a common base class. Virtual inheritance is a mechanism in C++ that helps address this problem by ensuring that there is only one instance of the common base class in the hierarchy.

#### 15. Can a class have both virtual and pure virtual functions?

**Answer:** Yes, a class can have both virtual and pure virtual functions. A class with pure virtual functions becomes an abstract class, and it can also provide concrete (non-pure) virtual functions with an implementation.

#### 16. Explain the concept of a "virtual pointer."

**Answer:** The virtual pointer (vptr) is a pointer maintained by the compiler in objects that have one or more virtual functions. It points to the vtable (virtual function table) associated with the object's type, allowing efficient dynamic dispatch during runtime.

#### 17. What is the role of the `final` specifier in C++?

**Answer:** The `final` specifier is used to indicate that a virtual function or a class cannot be overridden or further derived, respectively. It helps in enforcing design decisions and preventing unintended modifications in the inheritance hierarchy.

#### 18. Can a destructor be virtual in a base class and non-virtual in a derived class?

**Answer:** Yes, it is possible. While it is a good practice to make the destructor virtual in the base class if polymorphic behavior is expected, a derived class destructor does not need to be virtual if it does not introduce further polymorphism.

#### 19. How does the `typeid` operator work in C++?

**Answer:** The `typeid` operator in C++ is used to obtain information about the type of an expression or an object at runtime. It returns a `std::type_info` object that can be compared with other `type_info` objects to determine type compatibility.

#### 20. Explain the concept of covariance and contravariance in the context of virtual functions.

**Answer:** Covariance refers to the ability to return a derived class type from a virtual function declared in a base class, while contravariance refers to the ability to accept a base class type as a parameter in a virtual function declared in a derived class. C++ supports covariance in return types but does not support contravariance in parameter types for virtual functions.

####
