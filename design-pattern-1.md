# Design Pattern- 1

#### 1. What is a design pattern?

**Answer:** A design pattern is a reusable solution to a recurring design problem. It's a general guideline for solving common issues in software design. Design patterns help in creating maintainable and scalable software by providing proven development paradigms.

#### 2. Explain the Singleton design pattern.

**Answer:** The Singleton pattern ensures a class has only one instance and provides a global point to access it.

```cpp
class Singleton {
private:
    static Singleton* instance;
    Singleton() {}  // Private constructor to prevent instantiation.

public:
    static Singleton* getInstance() {
        if (!instance) {
            instance = new Singleton();
        }
        return instance;
    }
};
Singleton* Singleton::instance = nullptr;
```

#### 3. What is the Observer pattern?

**Answer:** The Observer pattern defines a one-to-many dependency between objects. When one object changes its state, all its dependents (observers) are notified and updated automatically.

```cpp
#include <iostream>
#include <vector>

class Observer {
public:
    virtual void update() = 0;
};

class Subject {
private:
    std::vector<Observer*> observers;

public:
    void addObserver(Observer* observer) {
        observers.push_back(observer);
    }

    void notifyObservers() {
        for (Observer* observer : observers) {
            observer->update();
        }
    }
};
```

#### 4. Explain the Factory Method design pattern.

**Answer:** The Factory Method pattern defines an interface for creating an object but leaves the choice of its type to the subclasses, creating the instance of the class.

```cpp
class Product {
public:
    virtual void display() = 0;
};

class ConcreteProduct : public Product {
public:
    void display() override {
        std::cout << "ConcreteProduct\n";
    }
};

class Creator {
public:
    virtual Product* createProduct() = 0;
};

class ConcreteCreator : public Creator {
public:
    Product* createProduct() override {
        return new ConcreteProduct();
    }
};
```

#### 5. What is the Strategy design pattern?

**Answer:** The Strategy pattern defines a family of algorithms, encapsulates each one, and makes them interchangeable. It lets the client vary its behavior independently from the context that uses it.

```cpp
class Strategy {
public:
    virtual void execute() = 0;
};

class ConcreteStrategyA : public Strategy {
public:
    void execute() override {
        std::cout << "Executing Strategy A\n";
    }
};

class Context {
private:
    Strategy* strategy;

public:
    Context(Strategy* strategy) : strategy(strategy) {}

    void setStrategy(Strategy* newStrategy) {
        strategy = newStrategy;
    }

    void executeStrategy() {
        strategy->execute();
    }
};
```

#### 6. Explain the Decorator design pattern.

**Answer:** The Decorator pattern attaches additional responsibilities to an object dynamically. Decorators provide a flexible alternative to subclassing for extending functionality.

```cpp
class Component {
public:
    virtual void operation() = 0;
};

class ConcreteComponent : public Component {
public:
    void operation() override {
        std::cout << "ConcreteComponent operation\n";
    }
};

class Decorator : public Component {
private:
    Component* component;

public:
    Decorator(Component* component) : component(component) {}

    void operation() override {
        component->operation();
    }
};

class ConcreteDecorator : public Decorator {
public:
    ConcreteDecorator(Component* component) : Decorator(component) {}

    void addedBehavior() {
        std::cout << "Added behavior\n";
    }

    void operation() override {
        Decorator::operation();
        addedBehavior();
    }
};
```

#### 7. What is the Adapter design pattern?

**Answer:** The Adapter pattern allows the interface of an existing class to be used as another interface. It is often used to make existing classes work with others without modifying their source code.

```cpp
class Target {
public:
    virtual void request() = 0;
};

class Adaptee {
public:
    void specificRequest() {
        std::cout << "Specific Request\n";
    }
};

class Adapter : public Target {
private:
    Adaptee* adaptee;

public:
    Adapter(Adaptee* adaptee) : adaptee(adaptee) {}

    void request() override {
        adaptee->specificRequest();
    }
};
```

#### 8. Explain the Composite design pattern.

**Answer:** The Composite pattern composes objects into tree structures to represent part-whole hierarchies. It allows clients to treat individual objects and compositions of objects uniformly.

```cpp
#include <iostream>
#include <vector>

class Component {
public:
    virtual void operation() = 0;
};

class Leaf : public Component {
public:
    void operation() override {
        std::cout << "Leaf operation\n";
    }
};

class Composite : public Component {
private:
    std::vector<Component*> children;

public:
    void add(Component* component) {
        children.push_back(component);
    }

    void operation() override {
        std::cout << "Composite operation\n";
        for (Component* component : children) {
            component->operation();
        }
    }
};
```

#### 9. What is the Command design pattern?

**Answer:** The Command pattern turns a request into a stand-alone object, containing all information about the request. This allows for parameterization of clients with different requests, queuing of requests, and logging of the requests.

```cpp
class Command {
public:
    virtual void execute() = 0;
};

class Receiver {
public:
    void action() {
        std::cout << "Receiver action\n";
    }
};

class ConcreteCommand : public Command {
private:
    Receiver* receiver;

public:
    ConcreteCommand(Receiver* receiver) : receiver(receiver) {}

    void execute() override {
        receiver->action();
    }
};

class Invoker {
private:
    Command* command;

public:
    void setCommand(Command* newCommand) {
        command = newCommand;
    }

    void executeCommand() {
        command->execute();
    }
};
```

#### 10. Explain the Proxy design pattern.

**Answer:** The Proxy pattern provides a surrogate or placeholder for another object to control access to it.

```cpp
class Subject {
public:
    virtual void request() = 0;
};

class RealSubject : public Subject {
public:
    void request() override {
        std::cout << "RealSubject request\n";
    }
};

class Proxy : public Subject {
private:
    RealSubject* realSubject;

public:
    Proxy() : realSubject(nullptr) {}

    void request() override {
        if (!realSubject) {
            realSubject = new RealSubject();
        }
        realSubject->request();
    }
};
```

These questions cover various design patterns, their concepts, and implementations. During interviews, it's important to not only provide code snippets but also explain the rationale behind the patterns and how they address specific design challenges.
