# Static - 2

11. **What is the difference between a static member variable and a static member function in a class?**
    * Answer: A static member variable is shared among all instances of a class, while a static member function operates on class-level rather than instance-level data. Static member variables store shared information, while static member functions perform operations that are not tied to a specific instance.
12. **Can you use the `static` keyword with a class constructor or destructor? If yes, how does it affect their behavior?**
    * Answer: No, the `static` keyword is not used with class constructors or destructors. Constructors and destructors are automatically called when objects are created and destroyed, respectively, without the need for explicit `static` modifiers.
13. **Explain the concept of static polymorphism in C++ with an example.**
    *   Answer: Static polymorphism refers to method overloading, which is resolved at compile-time. Compiler selects the appropriate function based on the number and types of arguments. Example:

        ```cpp
        class MathOperations {
        public:
            static int add(int a, int b) {
                return a + b;
            }
            
            static double add(double a, double b) {
                return a + b;
            }
        };
        ```
14. **How does the use of `static` affect the memory allocation for a variable in C++?**
    * Answer: A `static` variable in C++ has static storage duration, meaning it is allocated memory once, and the memory persists throughout the program's execution. It is initialized only once, and its value is retained between function calls.
15. **What is the purpose of a static\_cast in C++? Provide an example.**
    *   Answer: `static_cast` is used for explicit type conversions between compatible types. Example:

        ```cpp
        double myDouble = 3.14;
        int myInt = static_cast<int>(myDouble);
        ```
16. **How does the `static` keyword affect the visibility of functions in C++?**
    * Answer: When `static` is used with a function, it provides internal linkage, limiting its visibility to the translation unit where it is defined. The function is not visible outside that file.
17. **Explain the role of the `static` keyword in the context of a class member function.**
    * Answer: When used in a class definition, the `static` keyword indicates that the member function is associated with the class itself, not with instances of the class. It can be called using the class name without creating an object.
18. **What is the purpose of a static\_assert in C++? Provide an example.**
    *   Answer: `static_assert` is used for compile-time assertions. It triggers a compilation error if the specified condition is false. Example:

        ```cpp
        static_assert(sizeof(int) == 4, "int must be 4 bytes");
        ```
19. **Can you use the `static` keyword with a local function variable? If yes, what does it mean?**
    * Answer: No, the `static` keyword is not used with local function variables. It is used with variables at file scope or class scope to change their storage duration or linkage.
20. **How does the `static` keyword affect the initialization of variables in C++?**
    * Answer: When `static` is used with a variable, it changes the variable's storage duration to static. The variable is initialized only once, and its value is retained between function calls, making it suitable for maintaining state across multiple invocations.
