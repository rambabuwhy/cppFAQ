# Design Pattern-Flyweight

The Flyweight design pattern is a structural pattern that is used to minimize memory usage or computational expenses by sharing as much as possible with related objects. It is particularly useful when you have a large number of similar objects to manage. The key idea is to use a shared representation or "flyweight" for common state, and externalize the rest of the state into the context of the objects that need it.

Let's go through the Flyweight pattern example step by step:

1.  **Flyweight Interface:**

    ```cpp
    class Flyweight {
    public:
        virtual void operation() = 0;
    };
    ```

    This is the abstract base class defining the interface for flyweight objects. In this example, the `operation` method is a common operation that the flyweight objects will perform.
2.  **ConcreteFlyweight Class:**

    ```cpp
    class ConcreteFlyweight : public Flyweight {
    private:
        std::string intrinsicState;

    public:
        ConcreteFlyweight(const std::string& intrinsicState) : intrinsicState(intrinsicState) {}

        void operation() override {
            std::cout << "ConcreteFlyweight: " << intrinsicState << std::endl;
        }
    };
    ```

    This class is a concrete implementation of the `Flyweight` interface. It encapsulates the intrinsic state (state shared among flyweight objects). In this case, the `intrinsicState` is a `std::string`.
3.  **FlyweightFactory Class:**

    ```cpp
    class FlyweightFactory {
    private:
        std::unordered_map<std::string, Flyweight*> flyweights;

    public:
        Flyweight* getFlyweight(const std::string& key) {
            if (flyweights.find(key) == flyweights.end()) {
                flyweights[key] = new ConcreteFlyweight(key);
            }
            return flyweights[key];
        }
    };
    ```

    The `FlyweightFactory` class is responsible for managing the creation and reuse of flyweight objects. It uses an unordered map (`flyweights`) to keep track of created flyweights. The `getFlyweight` method checks if a flyweight with a given key (intrinsic state) already exists. If it does, it returns the existing flyweight; otherwise, it creates a new one and stores it in the map.
4.  **Client Code:**

    ```cpp
    int main() {
        FlyweightFactory factory;

        Flyweight* fw1 = factory.getFlyweight("A");
        Flyweight* fw2 = factory.getFlyweight("B");
        Flyweight* fw3 = factory.getFlyweight("A"); // Reuse existing flyweight

        fw1->operation();
        fw2->operation();
        fw3->operation();

        delete fw1;
        delete fw2;
        delete fw3;

        return 0;
    }
    ```

    In the client code, we create a `FlyweightFactory` instance and use it to get flyweights with intrinsic states "A" and "B". The key point is that when requesting a flyweight with intrinsic state "A" again, it reuses the existing flyweight instead of creating a new one. Finally, we call the `operation` method on each flyweight.

    The expected output would be:

    ```makefile
    makefileCopy codeConcreteFlyweight: A
    ConcreteFlyweight: B
    ConcreteFlyweight: A
    ```

This demonstrates the Flyweight pattern in action, where memory is saved by reusing shared flyweights for common intrinsic states.
