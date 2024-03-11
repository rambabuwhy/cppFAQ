# Design Pattern-Broker

The Broker design pattern is a structural pattern that defines a mediator (or broker) object that encapsulates the communication between multiple objects, allowing them to interact without being directly connected. This pattern promotes loose coupling and helps manage the complexity of communication between different components.

Let's break down the Broker design pattern implementation step by step:

#### 1. Define the Mediator Interface

```cpp
class Mediator {
public:
    virtual void sendMessage(const std::string& message, Colleague* colleague) const = 0;
};
```

Here, we define the `Mediator` interface with a pure virtual function `sendMessage`. This function will be implemented by concrete mediators and will be responsible for handling the communication between colleagues.

#### 2. Implement the Concrete Mediator

```cpp
class ConcreteMediator : public Mediator {
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

private:
    std::vector<Colleague*> colleagues;
};
```

The `ConcreteMediator` class implements the `Mediator` interface. It maintains a list of colleagues and implements the `sendMessage` function to distribute messages to all colleagues except the sender.

#### 3. Define the Colleague Interface

```cpp
class Colleague {
public:
    Colleague(Mediator* mediator, const std::string& name)
        : mediator(mediator), name(name) {}

    virtual void sendMessage(const std::string& message) const {
        mediator->sendMessage(message, this);
    }

    virtual void receiveMessage(const std::string& message) const {
        std::cout << name << " received message: " << message << std::endl;
    }

protected:
    Mediator* mediator;
    std::string name;
};
```

The `Colleague` class represents objects that can communicate through the mediator. It has a reference to the mediator and provides a `sendMessage` function to send messages through the mediator. The `receiveMessage` function is a virtual function to be implemented by concrete colleagues.

#### 4. Implement a Concrete Colleague

```cpp
class ConcreteColleague : public Colleague {
public:
    ConcreteColleague(Mediator* mediator, const std::string& name)
        : Colleague(mediator, name) {}

    void doSomething() {
        std::string message = "Hello, everyone!";
        sendMessage(message);
    }
};
```

The `ConcreteColleague` class is a concrete implementation of a colleague. It has a `doSomething` function that sends a message through the mediator when called.

#### 5. Client Code

```cpp
int main() {
    ConcreteMediator mediator;

    ConcreteColleague colleague1(&mediator, "Colleague 1");
    ConcreteColleague colleague2(&mediator, "Colleague 2");

    mediator.addColleague(&colleague1);
    mediator.addColleague(&colleague2);

    colleague1.doSomething();

    return 0;
}
```

In the `main` function, we create a `ConcreteMediator` and two `ConcreteColleague` instances. We add these colleagues to the mediator using the `addColleague` function. When `colleague1` calls `doSomething`, it sends a message through the mediator, and both colleagues receive the message.

This example demonstrates how the Broker design pattern facilitates communication between objects through a mediator, promoting loose coupling between them.
