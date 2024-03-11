# Design Pattern-Bridge

The Bridge design pattern is a structural pattern that separates the abstraction from its implementation so that both can vary independently. It involves creating a bridge interface, known as an abstraction, and implementing it with different concrete classes. This pattern is useful when you want to avoid a permanent binding between an abstraction and its implementation, allowing both to evolve independently.

Let's break down the Bridge design pattern example step by step:

1.  **Implementor Interface:**

    ```cpp
    class Implementor {
    public:
        virtual void implement() = 0;
    };
    ```

    Here, `Implementor` is an interface that declares a method `implement()`.
2.  **Concrete Implementors A and B:**

    ```cpp
    class ConcreteImplementorA : public Implementor {
    public:
        void implement() override {
            std::cout << "Concrete Implementor A" << std::endl;
        }
    };

    class ConcreteImplementorB : public Implementor {
    public:
        void implement() override {
            std::cout << "Concrete Implementor B" << std::endl;
        }
    };
    ```

    `ConcreteImplementorA` and `ConcreteImplementorB` are two classes implementing the `Implementor` interface. They provide specific implementations of the `implement()` method.
3.  **Abstraction Interface:**

    ```cpp
    class Abstraction {
    protected:
        Implementor* implementor;

    public:
        Abstraction(Implementor* impl) : implementor(impl) {}

        virtual void operation() = 0;
    };
    ```

    `Abstraction` is an interface that contains a reference to an `Implementor` object and declares a pure virtual method `operation()`.
4.  **Refined Abstractions A and B:**

    ```cpp
    class RefinedAbstractionA : public Abstraction {
    public:
        RefinedAbstractionA(Implementor* impl) : Abstraction(impl) {}

        void operation() override {
            std::cout << "Refined Abstraction A - ";
            implementor->implement();
        }
    };

    class RefinedAbstractionB : public Abstraction {
    public:
        RefinedAbstractionB(Implementor* impl) : Abstraction(impl) {}

        void operation() override {
            std::cout << "Refined Abstraction B - ";
            implementor->implement();
        }
    };
    ```

    `RefinedAbstractionA` and `RefinedAbstractionB` are concrete classes that extend `Abstraction` and provide specific implementations for the `operation()` method. They use the `Implementor` reference to delegate the `implement()` call.
5.  **Main Function:**

    ```cpp
    int main() {
        Implementor* implementorA = new ConcreteImplementorA();
        Implementor* implementorB = new ConcreteImplementorB();

        Abstraction* abstractionA = new RefinedAbstractionA(implementorA);
        Abstraction* abstractionB = new RefinedAbstractionB(implementorB);

        abstractionA->operation();
        abstractionB->operation();

        delete implementorA;
        delete implementorB;
        delete abstractionA;
        delete abstractionB;

        return 0;
    }
    ```

    In the `main()` function, we create instances of `ConcreteImplementorA` and `ConcreteImplementorB`. We then create instances of `RefinedAbstractionA` and `RefinedAbstractionB`, passing the corresponding `Implementor` instances.

    Finally, we call the `operation()` method on each refined abstraction, and they, in turn, delegate the `implement()` call to the specific `Implementor` class.

This example demonstrates how the Bridge pattern allows the abstraction and implementation to vary independently. New implementations or abstractions can be added without modifying existing code, promoting flexibility and maintainability.
