# Design Pattern-Mediator

The Mediator design pattern is a behavioral design pattern that defines an object that centralizes communication between various components, thus promoting loose coupling among them. The Mediator pattern is useful when a set of objects need to communicate with each other, but direct connections between them would create a complex and tangled structure.

Let's break down the Mediator design pattern implementation step by step:

1.  **Mediator Interface:**

    ```cpp
    class Mediator {
    public:
        virtual void sendMessage(const std::string& message, Colleague* sender) const = 0;
    };
    ```

    * `Mediator` is an abstract class that defines the interface for communication between colleagues.
    * It declares a pure virtual function `sendMessage` that concrete mediators must implement.
2.  **Colleague Interface:**

    ```cpp
    class Colleague {
    protected:
        Mediator* mediator;

    public:
        Colleague(Mediator* mediator) : mediator(mediator) {}

        virtual void sendMessage(const std::string& message) const = 0;
        virtual void receiveMessage(const std::string& message) const = 0;
    };
    ```

    * `Colleague` is an abstract class that represents the interface for concrete colleagues.
    * It has a protected member `mediator` to store the reference to the mediator.
    * Declares pure virtual functions `sendMessage` and `receiveMessage`.
3.  **Concrete Mediator Class:**

    ```cpp
    class ConcreteMediator : public Mediator {
    private:
        std::vector<Colleague*> colleagues;

    public:
        void addColleague(Colleague* colleague) {
            colleagues.push_back(colleague);
        }

        void sendMessage(const std::string& message, Colleague* sender) const override {
            for (Colleague* colleague : colleagues) {
                if (colleague != sender) {
                    colleague->receiveMessage(message);
                }
            }
        }
    };
    ```

    * `ConcreteMediator` implements the `Mediator` interface.
    * It keeps a list of colleagues and provides a method (`addColleague`) to add colleagues to the list.
    * The `sendMessage` method iterates through the list of colleagues, excluding the sender, and calls their `receiveMessage` method.
4.  **Concrete Colleague Class:**

    ```cpp
    class ConcreteColleague : public Colleague {
    public:
        ConcreteColleague(Mediator* mediator) : Colleague(mediator) {}

        void sendMessage(const std::string& message) const override {
            std::cout << "Colleague sends message: " << message << std::endl;
            mediator->sendMessage(message, this);
        }

        void receiveMessage(const std::string& message) const override {
            std::cout << "Colleague receives message: " << message << std::endl;
        }
    };
    ```

    * `ConcreteColleague` implements the `Colleague` interface.
    * The `sendMessage` method sends a message using the mediator and prints a log.
    * The `receiveMessage` method prints a log when a message is received.
5.  **Main Function:**

    ```cpp
    int main() {
        ConcreteMediator mediator;

        ConcreteColleague colleague1(&mediator);
        ConcreteColleague colleague2(&mediator);

        mediator.addColleague(&colleague1);
        mediator.addColleague(&colleague2);

        colleague1.sendMessage("Hello, colleague2!");
        colleague2.sendMessage("Hi, colleague1!");

        return 0;
    }
    ```

    * In the `main` function, a `ConcreteMediator` is created.
    * Two `ConcreteColleague` objects are instantiated with references to the mediator.
    * Colleagues are added to the mediator using the `addColleague` method.
    * Colleagues exchange messages using the `sendMessage` method, and the mediator handles the communication.

This example demonstrates the Mediator pattern by creating a simple communication system where colleagues can send messages to each other through a mediator, promoting loose coupling between them.
