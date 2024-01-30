# Design Pattern- 2

#### 11. What is the Template Method design pattern?

**Answer:** The Template Method pattern defines the skeleton of an algorithm in the superclass but lets subclasses override specific steps of the algorithm without changing its structure.

```cpp
#include <iostream>

class AbstractClass {
public:
    void templateMethod() {
        step1();
        step2();
        step3();
    }

    virtual void step1() = 0;
    virtual void step2() = 0;
    virtual void step3() = 0;
};

class ConcreteClass : public AbstractClass {
public:
    void step1() override {
        std::cout << "ConcreteClass Step 1\n";
    }

    void step2() override {
        std::cout << "ConcreteClass Step 2\n";
    }

    void step3() override {
        std::cout << "ConcreteClass Step 3\n";
    }
};
```

#### 12. Explain the State design pattern.

**Answer:** The State pattern allows an object to alter its behavior when its internal state changes. The object will appear to change its class.

```cpp
#include <iostream>

class State {
public:
    virtual void handle() = 0;
};

class ConcreteStateA : public State {
public:
    void handle() override {
        std::cout << "ConcreteStateA handled\n";
    }
};

class ConcreteStateB : public State {
public:
    void handle() override {
        std::cout << "ConcreteStateB handled\n";
    }
};

class Context {
private:
    State* currentState;

public:
    void setState(State* newState) {
        currentState = newState;
    }

    void request() {
        currentState->handle();
    }
};
```

#### 13. What is the Command design pattern?

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

#### 14. Explain the Chain of Responsibility design pattern.

**Answer:** The Chain of Responsibility pattern passes requests along a chain of handlers. Upon receiving a request, each handler decides either to process the request or to pass it to the next handler in the chain.

```cpp
#include <iostream>

class Handler {
private:
    Handler* successor;

public:
    Handler() : successor(nullptr) {}

    void setSuccessor(Handler* handler) {
        successor = handler;
    }

    virtual void handleRequest(int request) {
        if (successor) {
            successor->handleRequest(request);
        }
    }
};

class ConcreteHandlerA : public Handler {
public:
    void handleRequest(int request) override {
        if (request < 10) {
            std::cout << "ConcreteHandlerA handling request " << request << "\n";
        } else {
            Handler::handleRequest(request);
        }
    }
};

class ConcreteHandlerB : public Handler {
public:
    void handleRequest(int request) override {
        if (request >= 10 && request < 20) {
            std::cout << "ConcreteHandlerB handling request " << request << "\n";
        } else {
            Handler::handleRequest(request);
        }
    }
};
```

#### 15. What is the Visitor design pattern?

**Answer:** The Visitor pattern represents an operation to be performed on elements of an object structure. It lets you define a new operation without changing the classes of the elements on which it operates.

```cpp
class ElementA;
class ElementB;

class Visitor {
public:
    virtual void visitElementA(ElementA* element) = 0;
    virtual void visitElementB(ElementB* element) = 0;
};

class Element {
public:
    virtual void accept(Visitor* visitor) = 0;
};

class ElementA : public Element {
public:
    void accept(Visitor* visitor) override {
        visitor->visitElementA(this);
    }
};

class ElementB : public Element {
public:
    void accept(Visitor* visitor) override {
        visitor->visitElementB(this);
    }
};

class ConcreteVisitor : public Visitor {
public:
    void visitElementA(ElementA* element) override {
        std::cout << "ConcreteVisitor visiting ElementA\n";
    }

    void visitElementB(ElementB* element) override {
        std::cout << "ConcreteVisitor visiting ElementB\n";
    }
};
```

#### 16. Explain the Memento design pattern.

**Answer:** The Memento pattern provides the ability to restore an object to its previous state.

```cpp
#include <iostream>
#include <string>

class Memento {
private:
    std::string state;

public:
    Memento(const std::string& s) : state(s) {}

    const std::string& getState() const {
        return state;
    }
};

class Originator {
private:
    std::string state;

public:
    void setState(const std::string& s) {
        state = s;
    }

    Memento createMemento() {
        return Memento(state);
    }

    void restoreMemento(const Memento& memento) {
        state = memento.getState();
    }

    void showState() const {
        std::cout << "Current State: " << state << "\n";
    }
};

class Caretaker {
private:
    Memento memento;

public:
    void setMemento(const Memento& m) {
        memento = m;
    }

    const Memento& getMemento() const {
        return memento;
    }
};
```

#### 17. What is the Interpreter design pattern?

**Answer:** The Interpreter pattern defines a grammar for the language, as well as an interpreter that interprets sentences in the language.

```cpp
#include <iostream>
#include <unordered_map>

class Context {
public:
    bool lookup(const std::string& variable) const {
        return variables.find(variable) != variables.end();
    }

    void assign(const std::string& variable, bool value) {
        variables[variable] = value;
    }

private:
    std::unordered_map<std::string, bool> variables;
};

class AbstractExpression {
public:
    virtual bool interpret(Context& context) = 0;
};

class TerminalExpression : public AbstractExpression {
private:
    std::string variable;

public:
    TerminalExpression(const std::string& var) : variable(var) {}

    bool interpret(Context& context) override {
        return context.lookup(variable);
    }
};

class NonterminalExpression : public AbstractExpression {
private:
    AbstractExpression* expression;

public:
    NonterminalExpression(AbstractExpression* expr) : expression(expr) {}

    bool interpret(Context& context) override {
        return !expression->interpret(context);
    }
};
```

#### 18. Explain the Bridge design pattern.

**Answer:** The Bridge pattern separates abstraction from implementation so that both can vary independently.

```cpp
#include <iostream>

class Implementor {
public:
    virtual void operationImpl() = 0;
};

class ConcreteImplementorA : public Implementor {
public:
    void operationImpl() override {
        std::cout << "ConcreteImplementorA operation\n";
    }
};

class ConcreteImplementorB : public Implementor {
public:
    void operationImpl() override {
        std::cout << "ConcreteImplementorB operation\n";
    }
};

class Abstraction {
protected:
    Implementor* implementor;

public:
    Abstraction(Implementor* impl) : implementor(impl) {}

    virtual void operation() = 0;
};

class RefinedAbstraction : public Abstraction {
public:
    RefinedAbstraction(Implementor* impl) : Abstraction(impl) {}

    void operation() override {
        implementor->operationImpl();
    }
};
```

#### 19. What is the Mediator design pattern?

**Answer:** The Mediator pattern defines an object that centralizes communication between a set of objects. It promotes loose coupling by keeping objects from referring to each other explicitly.

```cpp
#include <iostream>
#include <string>

class Colleague;

class Mediator {
public:
    virtual void sendMessage(const Colleague* sender, const std::string& message) const = 0;
};

class Colleague {
protected:
    Mediator* mediator;

public:
    Colleague(Mediator* med) : mediator(med) {}

    virtual void sendMessage(const std::string& message) const {
        mediator->sendMessage(this, message);
    }

    virtual void receiveMessage(const std::string& message) const = 0;
};

class ConcreteColleagueA : public Colleague {
public:
    ConcreteColleagueA(Mediator* med) : Colleague(med) {}

    void receiveMessage(const std::string& message) const override {
        std::cout << "ConcreteColleagueA received: " << message << "\n";
    }
};

class ConcreteColleagueB : public Colleague {
public:
    ConcreteColleagueB(Mediator* med) : Colleague(med) {}

    void receiveMessage(const std::string& message) const override {
        std::cout << "ConcreteColleagueB received: " << message << "\n";
    }
};

class ConcreteMediator : public Mediator {
private:
    Colleague* colleagueA;
    Colleague* colleagueB;

public:
    void setColleagueA(Colleague* colleague) {
        colleagueA = colleague;
    }

    void setColleagueB(Colleague* colleague) {
        colleagueB = colleague;
    }

    void sendMessage(const Colleague* sender, const std::string& message) const override {
        if (sender == colleagueA) {
            colleagueB->receiveMessage(message);
        } else if (sender == colleagueB) {
            colleagueA->receiveMessage(message);
        }
    }
};
```

#### 20. Explain the Flyweight design pattern.

**Answer:** The Flyweight pattern minimizes memory usage or computational expenses by sharing as much as possible with related objects; it is used to support large numbers of similar objects efficiently.

```cpp
#include <iostream>
#include <unordered_map>

class Flyweight {
public:
    virtual void operation() = 0;
};

class ConcreteFlyweight : public Flyweight {
private:
    int intrinsicState;

public:
    ConcreteFlyweight(int state) : intrinsicState(state) {}

    void operation() override {
        std::cout << "ConcreteFlyweight with intrinsic state " << intrinsicState << "\n";
    }
};

class UnsharedConcreteFlyweight : public Flyweight {
private:
    int extrinsicState;

public:
    UnsharedConcreteFlyweight(int state) : extrinsicState(state) {}

    void operation() override {
        std::cout << "UnsharedConcreteFlyweight with extrinsic state " << extrinsicState << "\n";
    }
};

class FlyweightFactory {
private:
    std::unordered_map<int, Flyweight*> flyweights;

public:
    Flyweight* getFlyweight(int key) {
        if (flyweights.find(key) == flyweights.end()) {
            flyweights[key] = new ConcreteFlyweight(key);
        }
        return flyweights[key];
    }
};
```

These additional design pattern questions cover a range of patterns, providing a comprehensive understanding of common design patterns used in software development.