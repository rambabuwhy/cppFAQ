# Design Pattern-Strategy

The Strategy Design Pattern is a behavioral design pattern that defines a family of algorithms, encapsulates each algorithm, and makes them interchangeable. It lets the algorithm vary independently from the clients that use it.

Let's break down the implementation step by step:

1.  **Strategy (Abstract Base Class):**

    ```cpp
    class Strategy {
    public:
        virtual void execute() const = 0;
    };
    ```

    * This is the abstract base class that declares the interface for all concrete strategies.
    * The `execute` method is a pure virtual function, meaning it must be implemented by any concrete strategy.
2.  **Concrete Strategy Classes:**

    ```cpp
    class ConcreteStrategyA : public Strategy {
    public:
        void execute() const override {
            std::cout << "Executing Strategy A" << std::endl;
        }
    };

    class ConcreteStrategyB : public Strategy {
    public:
        void execute() const override {
            std::cout << "Executing Strategy B" << std::endl;
        }
    };
    ```

    * These are the concrete classes that inherit from the `Strategy` base class and provide specific implementations for the `execute` method.
3.  **Context Class:**

    ```cpp
    class Context {
    private:
        Strategy* strategy;

    public:
        Context(Strategy* strategy) : strategy(strategy) {}

        void setStrategy(Strategy* newStrategy) {
            strategy = newStrategy;
        }

        void executeStrategy() const {
            strategy->execute();
        }
    };
    ```

    * The `Context` class holds a reference to a strategy object.
    * The constructor takes an initial strategy.
    * The `setStrategy` method allows changing the strategy at runtime.
    * The `executeStrategy` method calls the `execute` method on the current strategy.
4.  **Client Code (main function):**

    ```cpp
    int main() {
        ConcreteStrategyA strategyA;
        ConcreteStrategyB strategyB;

        Context context(&strategyA);
        context.executeStrategy();

        context.setStrategy(&strategyB);
        context.executeStrategy();

        return 0;
    }
    ```

    * In the `main` function, we create instances of `ConcreteStrategyA` and `ConcreteStrategyB`.
    * We initialize a `Context` object with `strategyA` and execute its strategy.
    * We then change the strategy of the context to `strategyB` and execute it again.

This design allows you to encapsulate different algorithms (strategies) in separate classes, making it easy to extend and modify the behavior of the system without altering the client code. The client code can dynamically switch between different strategies at runtime.
