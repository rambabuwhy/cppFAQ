# Design Pattern-Chain of Responsibility

The Chain of Responsibility design pattern is a behavioral pattern that allows an object to pass a request along a chain of handlers. Each handler decides either to process the request or to pass it to the next handler in the chain. This pattern helps to decouple the sender of the request from its receivers.

Let's break down the implementation step by step:

#### 1. Handler Interface

```cpp
// Handler interface
class Handler {
public:
    virtual void setNext(Handler* nextHandler) = 0;
    virtual void handleRequest(const std::string& request) = 0;
};
```

* `Handler` is an abstract base class (interface) that declares two pure virtual functions: `setNext` and `handleRequest`.
* `setNext` is used to set the next handler in the chain.
* `handleRequest` is where the concrete handlers will provide their implementation for handling requests.

#### 2. ConcreteHandler Class

```cpp
// ConcreteHandler class
class ConcreteHandler : public Handler {
private:
    Handler* nextHandler;

public:
    ConcreteHandler() : nextHandler(nullptr) {}

    void setNext(Handler* nextHandler) override {
        this->nextHandler = nextHandler;
    }

    void handleRequest(const std::string& request) override {
        if (canHandle(request)) {
            std::cout << "ConcreteHandler handled the request: " << request << std::endl;
        } else if (nextHandler != nullptr) {
            std::cout << "Passing the request to the next handler." << std::endl;
            nextHandler->handleRequest(request);
        } else {
            std::cout << "No handler can process the request." << std::endl;
        }
    }

private:
    bool canHandle(const std::string& request) {
        // Add your specific conditions for handling the request
        return request == "specific_request";
    }
};
```

* `ConcreteHandler` is a concrete class that implements the `Handler` interface.
* It has a private member `nextHandler` which is a pointer to the next handler in the chain.
* `setNext` sets the next handler in the chain.
* `handleRequest` is where the concrete handling logic is implemented. If it can handle the request, it processes it; otherwise, it passes the request to the next handler in the chain.

#### 3. Main Function

```cpp
int main() {
    // Create handler objects
    ConcreteHandler handler1;
    ConcreteHandler handler2;
    ConcreteHandler handler3;

    // Set up the chain of responsibility
    handler1.setNext(&handler2);
    handler2.setNext(&handler3);

    // Make requests
    handler1.handleRequest("some_request");
    handler1.handleRequest("specific_request");
    handler1.handleRequest("another_request");

    return 0;
}
```

* In the `main` function, three instances of `ConcreteHandler` are created: `handler1`, `handler2`, and `handler3`.
* The chain of responsibility is set up by calling `setNext` on each handler, linking them together.
* Three requests are then made to the first handler in the chain (`handler1`) using `handleRequest`. The requests are "some\_request," "specific\_request," and "another\_request."

#### Output

The output of the program will demonstrate how the chain of responsibility processes or passes the requests based on the conditions defined in the `canHandle` method of the `ConcreteHandler` class. The output might look like this:

```vbnet
No handler can process the request.
ConcreteHandler handled the request: specific_request
Passing the request to the next handler.
```

\
