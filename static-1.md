# Static - 1

1. **What is the purpose of the `static` keyword in C++?**
   * Answer: `static` is used to declare static members in a class, to define variables with static storage duration, and to limit the scope of a function or variable to the current translation unit.
2. **Explain the difference between a static member function and a non-static member function in a C++ class.**
   * Answer: A static member function is associated with the class itself, not with a particular instance. It can be called using the class name without creating an object. A non-static member function is associated with an instance of the class and can be called using an object of the class.
3. **What is the lifetime of a static variable in a function?**
   * Answer: Static variables in a function have a lifetime that spans the entire program execution. They are initialized only once and retain their values between function calls.
4. **How does the use of `static` affect the linkage of a variable or function?**
   * Answer: When `static` is used with a variable or function, it gives internal linkage, limiting its visibility to the current translation unit. This means the variable or function is not accessible from other files.
5. **Explain the role of the `static` keyword in the context of a global variable.**
   * Answer: When `static` is used with a global variable, it limits its scope to the file where it is defined, providing internal linkage and making it inaccessible from other files.
6. **What is a static member of a class, and how is it different from a non-static member?**
   * Answer: A static member in a class is shared among all instances of the class, while a non-static member is unique to each instance. Static members are associated with the class itself rather than with instances.
7. **What is the purpose of a static constructor in C++?**
   * Answer: C++ does not have static constructors like some other languages. However, you may be referring to the initialization of static variables, which is done once during the program's startup before the `main` function is called.
8. **Can you use the `static` keyword with a local variable inside a function? If yes, what does it mean?**
   * Answer: Yes, you can use the `static` keyword with a local variable inside a function. When applied to a local variable, it changes the variable's storage duration to static, meaning it retains its value between function calls.
9. **Explain the concept of static binding and dynamic binding in C++.**
   * Answer: Static binding (compile-time binding) is resolved during compile-time, and it is associated with function overloading and early binding. Dynamic binding (runtime binding) is resolved during runtime and is related to function overriding and late binding. The `static` keyword is not directly related to these concepts but can be involved in achieving certain behaviors.
10. **How can you use the `static` keyword to create a counter for instances of a class?**

    * Answer: By using a `static` member variable in the class and incrementing it in the constructor, you can create a counter that keeps track of the number of instances created.

