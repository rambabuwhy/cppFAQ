# Design Pattern-Composite

The Composite Design Pattern is a structural pattern that lets you compose objects into tree structures to represent part-whole hierarchies. It allows clients to treat individual objects and compositions of objects uniformly. This pattern is particularly useful when you want clients to treat individual objects and compositions of objects in a uniform manner.

Let's break down the implementation step by step:

1.  **Component Class:**

    ```cpp
    class Component {
    public:
        virtual void operation() const = 0;
        virtual ~Component() = default;
    };
    ```

    * `Component` is an abstract base class that declares the interface for both leaf and composite objects.
    * It has a pure virtual function `operation()` that must be implemented by its derived classes.
    * The virtual destructor ensures proper cleanup when objects are deleted through a pointer to the base class.
2.  **Leaf Class:**

    ```cpp
    class Leaf : public Component {
    public:
        void operation() const override {
            std::cout << "Leaf operation\n";
        }
    };
    ```

    * `Leaf` is a concrete class derived from `Component`.
    * It implements the `operation()` function to define the behavior of individual objects.
3.  **Composite Class:**

    ```cpp
    class Composite : public Component {
    private:
        std::list<Component*> children;

    public:
        void add(Component* component) {
            children.push_back(component);
        }

        void remove(Component* component) {
            children.remove(component);
        }

        void operation() const override {
            std::cout << "Composite operation\n";
            for (const auto& child : children) {
                child->operation();
            }
        }
    };
    ```

    * `Composite` is a concrete class derived from `Component`.
    * It contains a list of `Component` pointers, representing the children (either leaves or other composites).
    * `add()` and `remove()` methods allow adding and removing child components.
    * The `operation()` function iterates through its children, calling their `operation()` functions, providing a uniform way to handle both leaves and composites.
4.  **Main Function:**

    ```cpp
    int main() {
        Leaf leaf1, leaf2, leaf3;
        Composite composite;
        Composite composite2;

        composite.add(&leaf1);
        composite.add(&leaf2);

        composite2.add(&leaf3);
        composite2.add(&composite);

        leaf1.operation();
        composite.operation();
        composite2.operation();

        return 0;
    }
    ```

    * In the `main()` function, we create instances of `Leaf`, `Composite`, and `Composite2`.
    * We add leaf objects to the first composite (`composite`), and then add `leaf3` and the first composite to the second composite (`composite2`).
    * We demonstrate calling the `operation()` function on individual leaf and composite objects, showing the uniform treatment of both types of objects.

When you run this program, you should see output similar to the following:

```
Leaf operation
Composite operation
Leaf operation
Leaf operation
```

This output illustrates that the `operation()` function is called on both individual leaf objects and composite objects, demonstrating the flexibility and uniformity achieved through the Composite Design Pattern.
