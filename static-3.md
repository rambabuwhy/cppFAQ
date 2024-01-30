# Static - 3

21. **Explain the use of `static` in the context of file scope.**
    * Answer: When `static` is used at file scope (outside of any function or class), it limits the visibility of the variable or function to the translation unit where it is defined. This provides internal linkage and makes the variable or function inaccessible from other files.
22. **How does the `static` keyword impact the lifetime of a variable?**
    * Answer: The `static` keyword affects the lifetime of a variable by giving it static storage duration. The variable is initialized only once, and its memory persists throughout the program's execution, retaining its value between function calls.
23. **What is the purpose of the `static` keyword when used with a member variable in a class?**
    * Answer: When used with a member variable in a class, the `static` keyword indicates that the variable is shared among all instances of the class. It exists at the class level rather than at the instance level.
24. **Explain the difference between a `const static` member variable and a `static const` member variable in a class.**
    * Answer: Both are used to declare constant static member variables in a class. The difference lies in the order: `const static` emphasizes that the variable is constant, while `static const` emphasizes its static nature. However, the two are usually interchangeable.
25. **How is a `static` member function different from a global function in C++?**
    * Answer: A `static` member function is associated with a class and can access its `static` members. It is invoked using the class name. A global function is not associated with any class and operates independently of class-specific data.
26. **In what situations would you use a `static` local variable inside a function?**
    * Answer: `static` local variables are used when you want a variable to retain its value between function calls. It is initialized only once and persists throughout the program's execution.
27. **What is the purpose of the `thread_local` keyword, and how does it differ from `static` variables?**
    * Answer: `thread_local` is used to declare thread-local storage duration, meaning each thread has its own instance of the variable. This is different from `static` variables, which are shared among all threads.
28. **How does the use of `static` affect the visibility of a class in C++?**
    * Answer: The `static` keyword, when applied to a class, makes its members `static`. This means they are associated with the class itself rather than with instances of the class. It doesn't affect the visibility of the class itself.
29. **Explain the concept of static linkage and dynamic linkage in C++ with respect to functions.**
    * Answer: Static linkage (compile-time linkage) is associated with `static` functions, where the binding is resolved at compile time. Dynamic linkage (runtime linkage) is associated with non-`static` functions, where the binding is resolved at runtime.
30. **Can you use the `static` keyword with a parameter in a function? If yes, what does it mean?**
    * Answer: No, the `static` keyword is not used with function parameters. It is used with variables at file scope, class scope, or local scope within functions to specify storage duration and linkage.
