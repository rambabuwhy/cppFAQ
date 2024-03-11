# Design Pattern-Command

The Command Design Pattern is a behavioral design pattern that turns a request into a stand-alone object, allowing for parameterization of clients with different requests, queuing of requests, and logging of the requests.

In the Command Design Pattern, the idea is to encapsulate a request as an object, turning it into a stand-alone entity that can be passed around and manipulated independently. This enables the decoupling of the sender of a request (Invoker) from the object that performs the action (Receiver).

In the example provided:

1.  **Command Interface:**

    ```cpp
    // Command interface
    class Command {
    public:
        virtual void execute() = 0;
    };
    ```

    The `Command` class is an interface that declares a single method `execute()`. This method represents the action to be performed.
2.  **ConcreteCommand:**

    ```cpp
    // Concrete Command class
    class ConcreteCommand : public Command {
    private:
        // Reference to the Receiver object
        // This is the object that will perform the actual action
        Receiver& receiver;

    public:
        ConcreteCommand(Receiver& receiver) : receiver(receiver) {}

        // Implementation of the execute method
        void execute() override {
            receiver.performAction();
        }
    };
    ```

    The `ConcreteCommand` class implements the `Command` interface and holds a reference to the `Receiver` object. In the `execute()` method, it calls the `performAction()` method on the `Receiver` object, effectively encapsulating the request to perform an action.
3.  **Invoker:**

    ```cpp
    // Invoker class
    class Invoker {
    private:
        // Command reference
        Command& command;

    public:
        Invoker(Command& command) : command(command) {}

        // Method to invoke the command
        void invoke() {
            command.execute();
        }
    };
    ```

    The `Invoker` class holds a reference to a `Command` object. It has a method called `invoke()` that, when called, triggers the `execute()` method on the associated `Command`. The `Invoker` is unaware of the specific details of the action; it simply invokes the command without knowing what it does.

Now, when you create a `ConcreteCommand` object and associate it with a `Receiver`, you have effectively turned the request (performing an action) into a stand-alone object (`ConcreteCommand`). This object can be passed around, stored, and manipulated independently of the original sender or the object that performs the action. The `Invoker` acts as the bridge, invoking the command without needing to know the details of how the action is performed. This encapsulation and separation of concerns are key aspects of the Command Design Pattern.
