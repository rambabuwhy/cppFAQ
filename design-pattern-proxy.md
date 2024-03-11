# Design Pattern- Proxy

The Proxy design pattern is a structural pattern that provides a surrogate or placeholder for another object to control access to it. This can be useful in various situations, such as controlling access permissions, lazy loading of resources, or adding additional functionality before or after the actual operation of the real object.

Let's break down the Proxy design pattern example step by step:

1.  **Subject Interface:**

    ```cpp
    class Subject {
    public:
        virtual void request() const = 0;
    };
    ```

    This is the interface that both the real object (`RealSubject`) and the proxy object (`Proxy`) implement. It declares a pure virtual function `request()` that represents the operation that the proxy will control access to.
2.  **RealSubject Class:**

    ```cpp
    class RealSubject : public Subject {
    public:
        void request() const override {
            std::cout << "RealSubject: Handling request\n";
        }
    };
    ```

    `RealSubject` is the class representing the real object. It inherits from the `Subject` interface and provides the implementation for the `request()` function. In this simple example, it prints a message indicating that it is handling the request.
3.  **Proxy Class:**

    ```cpp
    class Proxy : public Subject {
    private:
        RealSubject realSubject;

    public:
        void request() const override {
            std::cout << "Proxy: Checking access\n";
            realSubject.request();
        }
    };
    ```

    The `Proxy` class also inherits from the `Subject` interface, indicating that it can be used wherever a `Subject` is expected. It contains a private instance of `RealSubject` and implements the `request()` function. In this case, before calling `realSubject.request()`, it prints a message indicating that it is checking access.
4.  **Main Function:**

    ```cpp
    int main() {
        // Using the RealSubject directly
        RealSubject realObject;
        realObject.request();

        std::cout << "\n";
    ```

    ```cpp
        // Using the Proxy
        Proxy proxyObject;
        proxyObject.request();

        return 0;
      }
    ```

In the `main` function, we first create an instance of `RealSubject` called `realObject` and directly call its `request()` function. This demonstrates using the real object without any proxy.

Then, we create an instance of `Proxy` called `proxyObject` and call its `request()` function. The proxy, before delegating the request to the real object (`RealSubject`), prints a message indicating that it is checking access. This showcases the proxy controlling access to the real object.

5.  **Output:**

    ```makefile
    RealSubject: Handling request

    Proxy: Checking access
    RealSubject: Handling request
    ```

    The output shows that when using the real object directly, it handles the request. When using the proxy, the proxy first checks access before delegating the request to the real object.

This example is a basic illustration of the Proxy design pattern. Depending on your requirements, you can extend the proxy to add more complex behavior, such as lazy loading, access control, logging, or any other functionality needed to control or enhance the behavior of the real object.
