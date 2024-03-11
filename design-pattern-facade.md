# Design Pattern-Facade

The Facade Design Pattern is a structural pattern that provides a simplified interface to a set of interfaces in a subsystem, making it easier to use. It involves creating a unified interface that wraps a set of interfaces in a subsystem, thus making the subsystem easier to use for clients.

Let's break down the Facade Design Pattern example step by step:

1.  **Subsystem Classes:**

    * We have two subsystem classes, `Subsystem1` and `Subsystem2`, each representing a set of related operations or functionalities.

    ```cpp
    // Subsystem class 1
    class Subsystem1 {
    public:
        void operation1() {
            std::cout << "Subsystem1: Operation 1\n";
        }

        void operation2() {
            std::cout << "Subsystem1: Operation 2\n";
        }
    };

    // Subsystem class 2
    class Subsystem2 {
    public:
        void operation1() {
            std::cout << "Subsystem2: Operation 1\n";
        }

        void operation2() {
            std::cout << "Subsystem2: Operation 2\n";
        }
    };
    ```
2.  **Facade Class:**

    * The `Facade` class is created to provide a simplified interface for the client. It encapsulates instances of the subsystem classes.

    ```cpp
    // Facade class
    class Facade {
    public:
        Facade() {
            subsystem1 = new Subsystem1();
            subsystem2 = new Subsystem2();
        }

        ~Facade() {
            delete subsystem1;
            delete subsystem2;
        }

        // Facade methods that simplify the interface for the client
        void operation() {
            std::cout << "Facade: Operation\n";
            subsystem1->operation1();
            subsystem1->operation2();
            subsystem2->operation1();
            subsystem2->operation2();
        }

    private:
        Subsystem1* subsystem1;
        Subsystem2* subsystem2;
    };
    ```

    * The `Facade` class has methods that perform operations using the subsystems. The idea is to provide a higher-level, simplified interface for the client.
3.  **Client Code:**

    * In the `main` function, the client creates an instance of the `Facade` class and uses it to perform operations.

    ```cpp
    // Client code
    int main() {
        Facade facade;
        facade.operation();

        return 0;
    }
    ```

    * The client doesn't need to interact directly with the subsystems (`Subsystem1` and `Subsystem2`). Instead, it uses the `Facade` to perform the desired operation. In this example, the client calls the `operation` method on the `Facade` object.
4.  **Output:**

    * When the client runs, it will produce the following output:

    ```makefile
    Facade: Operation
    Subsystem1: Operation 1
    Subsystem1: Operation 2
    Subsystem2: Operation 1
    Subsystem2: Operation 2
    ```

    * The client gets the desired functionality without needing to understand or manage the intricacies of the subsystems. The `Facade` class acts as a simplified entry point.
