# Detail-7-purevirtual

In C++, the syntax "function() = 0" and "function() = default" are related to pure virtual functions and defaulted functions, respectively, but they serve different purposes.

1. `function() = 0` (Pure Virtual Function):
   * This syntax is used in the declaration of a pure virtual function in an abstract base class.
   * A pure virtual function is a virtual function that is declared in a base class but has no implementation in that class.
   * Classes containing pure virtual functions are abstract, and they cannot be instantiated. Derived classes must provide an implementation for these pure virtual functions to become concrete and be instantiated.
   *   Example:

       ```cpp
       class AbstractClass {
       public:
           virtual void pureVirtualFunction() = 0;
       };
       ```
2. `function() = default` (Defaulted Function):
   * This syntax is used to explicitly request the compiler to generate the default implementation for a special member function (like a default constructor, destructor, copy constructor, etc.).
   * It is often used in the implementation of the class, indicating that you want the compiler-generated default behavior for that particular function.
   *   Example:

       ```cpp
       class MyClass {
       public:
           // Use default implementation for the default constructor
           MyClass() = default;
           
           // Use default implementation for the copy constructor
           MyClass(const MyClass&) = default;
           
           // Use default implementation for the destructor
           ~MyClass() = default;
       };
       ```

In summary, "function() = 0" is used for pure virtual functions in abstract base classes, while "function() = default" is used to request the default implementation of certain special member functions in the class.
