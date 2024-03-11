# Design Pattern-Template

The Template Method design pattern is a behavioral design pattern that defines the skeleton of an algorithm in the base class but lets subclasses override specific steps of the algorithm without changing its structure. This pattern is useful when you have an algorithm that has a common structure across multiple classes, but some steps may vary.

Let's break down the example step by step:

1.  **AbstractClass Definition:**

    ```cpp
    class AbstractClass {
    public:
        void templateMethod() {
            step1();
            step2();
            step3();
        }

        virtual void step1() = 0;
        virtual void step2() = 0;
        virtual void step3() = 0;
    };
    ```

    * `AbstractClass` declares a template method `templateMethod()` that defines the high-level algorithm with three steps: `step1()`, `step2()`, and `step3()`.
    * The steps are declared as pure virtual functions, indicating that concrete subclasses must provide their implementations.
2.  **ConcreteClass1 Definition:**

    ```cpp
    class ConcreteClass1 : public AbstractClass {
    public:
        void step1() override {
            std::cout << "ConcreteClass1 - Step 1" << std::endl;
        }

        void step2() override {
            std::cout << "ConcreteClass1 - Step 2" << std::endl;
        }

        void step3() override {
            std::cout << "ConcreteClass1 - Step 3" << std::endl;
        }
    };
    ```

    * `ConcreteClass1` inherits from `AbstractClass` and provides concrete implementations for `step1()`, `step2()`, and `step3()`.
3.  **ConcreteClass2 Definition:**

    ```cpp
    class ConcreteClass2 : public AbstractClass {
    public:
        void step1() override {
            std::cout << "ConcreteClass2 - Step 1" << std::endl;
        }

        void step2() override {
            std::cout << "ConcreteClass2 - Step 2" << std::endl;
        }

        void step3() override {
            std::cout << "ConcreteClass2 - Step 3" << std::endl;
        }
    };
    ```

    * `ConcreteClass2` is similar to `ConcreteClass1`, providing its own implementations for `step1()`, `step2()`, and `step3()`.
4.  **Main Function:**

    ```cpp
    int main() {
        ConcreteClass1 concrete1;
        ConcreteClass2 concrete2;

        concrete1.templateMethod();
        // Output:
        // ConcreteClass1 - Step 1
        // ConcreteClass1 - Step 2
        // ConcreteClass1 - Step 3

        std::cout << std::endl;

        concrete2.templateMethod();
        // Output:
        // ConcreteClass2 - Step 1
        // ConcreteClass2 - Step 2
        // ConcreteClass2 - Step 3

        return 0;
    }
    ```

    * In the `main()` function, we create instances of `ConcreteClass1` and `ConcreteClass2`.
    * We then call the `templateMethod()` for each instance, which in turn executes the algorithm defined in `AbstractClass`.
    * The output shows that the template method is called, and the specific steps are executed according to the implementations in each concrete class.

In summary, the Template Method pattern allows you to define a common algorithm structure in a base class while allowing concrete subclasses to provide their implementations for specific steps of the algorithm.
