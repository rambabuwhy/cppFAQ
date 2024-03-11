# Design Pattern-State

The State design pattern is a behavioral design pattern that allows an object to alter its behavior when its internal state changes. The pattern involves defining a set of states, encapsulating the behavior associated with each state, and allowing the object to transition between states as its internal state changes.

Let's break down the State design pattern implementation step by step:

1.  **State Interface:**

    * Define an abstract base class `State` that declares the interface for handling requests. In this example, it's a simple `handleRequest` method.

    ```cpp
    class State {
    public:
        virtual void handleRequest(Context* context) = 0;
    };
    ```
2.  **Concrete State Classes:**

    * Create concrete classes (`ConcreteStateA` and `ConcreteStateB`) that implement the `State` interface. Each concrete state provides its own implementation of the `handleRequest` method.

    ```cpp
    class ConcreteStateA : public State {
    public:
        void handleRequest(Context* context) override {
            std::cout << "ConcreteStateA handling request." << std::endl;
            // Optionally, change the state of the context
            context->setState(std::make_shared<ConcreteStateB>());
        }
    };

    class ConcreteStateB : public State {
    public:
        void handleRequest(Context* context) override {
            std::cout << "ConcreteStateB handling request." << std::endl;
            // Optionally, change the state of the context
            context->setState(std::make_shared<ConcreteStateA>());
        }
    };
    ```
3.  **Context Class:**

    * Create a `Context` class that maintains a reference to the current state. The `Context` class delegates the handling of requests to the current state.

    ```cpp
    class Context {
    public:
        Context(std::shared_ptr<State> initialState) : currentState(initialState) {}

        void setState(std::shared_ptr<State> newState) {
            currentState = newState;
        }

        void request() {
            currentState->handleRequest(this);
        }

    private:
        std::shared_ptr<State> currentState;
    };
    ```
4.  **Client Code:**

    * In the `main` function, create an instance of the `Context` class with an initial state (`ConcreteStateA` in this case).
    * Perform some requests on the context, which will delegate the request handling to the current state.

    ```cpp
    int main() {
        // Create context with an initial state
        Context context(std::make_shared<ConcreteStateA>());

        // Perform some requests, changing the state
        context.request();
        context.request();
        context.request();

        return 0;
    }
    ```
5.  **Output:**

    * When you run the program, you will see the output indicating the handling of requests and the transition between states.

    ```
    ConcreteStateA handling request.
    ConcreteStateB handling request.
    ConcreteStateA handling request.
    ```

In summary, the State design pattern allows an object to alter its behavior by changing its internal state, and it promotes a clean separation of concerns by encapsulating each state's behavior in separate classes. The `Context` class delegates the handling of requests to the current state, and the states can change dynamically based on the context's requirements.
