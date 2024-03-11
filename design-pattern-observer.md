# Design Pattern-Observer

The Observer pattern is a behavioral design pattern where an object, known as the subject, maintains a list of its dependents, called observers, that are notified of any changes in the subject's state. This pattern is useful for implementing distributed event handling systems, where one object (the subject) changes state, and all its dependents (observers) are notified and updated automatically.

Let's break down the implementation step by step:

1.  **Observer Interface:**

    ```cpp
    class Observer {
    public:
        virtual void update(const std::string& message) = 0;
    };
    ```

    * Defines an interface for observers. In this case, it has a pure virtual function `update`, which will be called when the subject's state changes.
2.  **Concrete Observer:**

    ```cpp
    class ConcreteObserver : public Observer {
    public:
        ConcreteObserver(const std::string& name) : name(name) {}

        void update(const std::string& message) override {
            std::cout << name << " received message: " << message << std::endl;
        }

    private:
        std::string name;
    };
    ```

    * Implements the `Observer` interface with a concrete class.
    * Stores a name for the observer.
    * The `update` function prints a message indicating that the observer received a message.
3.  **Subject Interface:**

    ```cpp
    class Subject {
    public:
        virtual void attach(Observer* observer) = 0;
        virtual void detach(Observer* observer) = 0;
        virtual void notify(const std::string& message) = 0;
    };
    ```

    * Defines an interface for subjects. It has pure virtual functions for attaching, detaching, and notifying observers.
4.  **Concrete Subject:**

    ```cpp
    class ConcreteSubject : public Subject {
    public:
        void attach(Observer* observer) override {
            observers.push_back(observer);
        }

        void detach(Observer* observer) override {
            auto it = std::find(observers.begin(), observers.end(), observer);
            if (it != observers.end()) {
                observers.erase(it);
            }
        }

        void notify(const std::string& message) override {
            for (auto observer : observers) {
                observer->update(message);
            }
        }

        void changeState(const std::string& newState) {
            state = newState;
            notify("State changed to: " + newState);
        }

    private:
        std::vector<Observer*> observers;
        std::string state;
    };
    ```

    * Implements the `Subject` interface with a concrete class.
    * Stores a vector of observers.
    * Provides methods to attach, detach, and notify observers.
    * The `changeState` method changes the subject's state and notifies observers about the state change.
5.  **Main Function:**

    ```cpp
    int main() {
        ConcreteSubject subject;

        ConcreteObserver observer1("Observer 1");
        ConcreteObserver observer2("Observer 2");

        subject.attach(&observer1);
        subject.attach(&observer2);

        subject.changeState("New State 1");

        subject.detach(&observer1);

        subject.changeState("New State 2");

        return 0;
    }
    ```

    * Creates a `ConcreteSubject` object.
    * Creates two `ConcreteObserver` objects.
    * Attaches both observers to the subject.
    * Changes the subject's state, triggering a notification to all attached observers.
    * Detaches one observer (`observer1`).
    * Changes the state again, notifying only the remaining observer (`observer2`).

This example demonstrates the Observer pattern, where the observers (`ConcreteObserver` instances) are notified of changes in the subject's (`ConcreteSubject` instance) state. The output should show messages indicating the state changes received by the observers.
