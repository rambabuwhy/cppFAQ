# Design Pattern-Adapter

The Adapter design pattern is a structural pattern that allows the interface of an existing class to be used as another interface. It is often used to make existing classes work with others without modifying their source code. This pattern involves a single class called the adapter, which is responsible for joining functionalities of independent or incompatible interfaces.

Let's go through the example step by step:

1.  **Define the Target Interface:**

    ```cpp
    // Target interface that the client code expects
    class Target {
    public:
        virtual void request() const = 0;
    };
    ```

    Here, `Target` is an abstract class with a pure virtual function `request()`. This is the interface that the client code expects to work with.
2.  **Create the Adaptee Class:**

    ```cpp
    // Adaptee class that has a different interface
    class Adaptee {
    public:
        void specificRequest() const {
            std::cout << "Adaptee's specific request" << std::endl;
        }
    };
    ```

    `Adaptee` is an existing class with a method `specificRequest()`. This class has a different interface than what the client code expects.
3.  **Implement the Adapter Class:**

    ```cpp
    // Adapter class that adapts the Adaptee to the Target interface
    class Adapter : public Target {
    private:
        Adaptee* adaptee;

    public:
        Adapter(Adaptee* adaptee) : adaptee(adaptee) {}

        void request() const override {
            // Call the specificRequest method of Adaptee
            adaptee->specificRequest();
        }
    };
    ```

    `Adapter` is a class that inherits from `Target`. It has a private member variable `adaptee`, which is an instance of the `Adaptee` class. The `request()` method of the `Target` interface is implemented by delegating the call to the `specificRequest()` method of the `Adaptee`.
4.  **Client Code:**

    ```cpp
    int main() {
        // Create an instance of Adaptee
        Adaptee adaptee;

        // Create an Adapter and pass the Adaptee instance to it
        Adapter adapter(&adaptee);

        // Call the request method on the Target interface through the Adapter
        adapter.request();

        return 0;
    }
    ```

    In the `main()` function, an instance of `Adaptee` is created. Then, an `Adapter` is instantiated, taking the `Adaptee` instance as a parameter. Finally, the `request()` method is called on the `Adapter`, and internally it delegates the call to the `specificRequest()` method of the `Adaptee`.

The output of this program would be:

```rust
Adaptee's specific request
```

This demonstrates how the Adapter pattern allows the client code to use the `Target` interface to interact with the existing `Adaptee` class without modifying the `Adaptee`'s source code. The `Adapter` acts as a bridge between the two interfaces, making them compatible.
