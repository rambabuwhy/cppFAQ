# Design Pattern-Visitor

The Visitor design pattern is a behavioral pattern that allows you to define a new operation without changing the classes of the elements on which it operates. It is useful when you have a set of classes with a common interface, and you want to perform different operations on these classes without modifying their code.

Let's break down the Visitor pattern example step by step:

1.  **Define the Element Interface:**

    ```cpp
    class Element {
    public:
        virtual void accept(Visitor& visitor) = 0;
    };
    ```

    The `Element` interface declares the `accept` method, which will be implemented by concrete elements. This method accepts a `Visitor` as an argument.
2.  **Create Concrete Element Classes:**

    ```cpp
    class ConcreteElementA : public Element {
    public:
        void accept(Visitor& visitor) override {
            visitor.visit(*this);
        }

        void operationA() {
            std::cout << "Operation A on ConcreteElementA\n";
        }
    };

    class ConcreteElementB : public Element {
    public:
        void accept(Visitor& visitor) override {
            visitor.visit(*this);
        }

        void operationB() {
            std::cout << "Operation B on ConcreteElementB\n";
        }
    };
    ```

    Concrete elements (`ConcreteElementA` and `ConcreteElementB`) implement the `Element` interface. They provide an implementation for the `accept` method, calling the corresponding `visit` method of the provided `Visitor`.
3.  **Define the Visitor Interface:**

    ```cpp
    class Visitor {
    public:
        virtual void visit(ConcreteElementA& element) = 0;
        virtual void visit(ConcreteElementB& element) = 0;
    };
    ```

    The `Visitor` interface declares a `visit` method for each concrete element type. Concrete visitors will provide implementations for these methods, specifying the operations to be performed on each element.
4.  **Create Concrete Visitor Class:**

    ```cpp
    class ConcreteVisitor : public Visitor {
    public:
        void visit(ConcreteElementA& element) override {
            element.operationA();
        }

        void visit(ConcreteElementB& element) override {
            element.operationB();
        }
    };
    ```

    The `ConcreteVisitor` class implements the `Visitor` interface by providing specific implementations for each `visit` method. In this example, it performs different operations (`operationA` and `operationB`) on the concrete elements.
5.  **Usage in Main Function:**

    ```cpp
    int main() {
        ConcreteElementA elementA;
        ConcreteElementB elementB;
        ConcreteVisitor visitor;

        elementA.accept(visitor);
        elementB.accept(visitor);

        return 0;
    }
    ```

    In the `main` function, we create instances of `ConcreteElementA` and `ConcreteElementB`, as well as a `ConcreteVisitor`. We then call the `accept` method on each element, passing the visitor as an argument. The visitor, in turn, performs the appropriate operation on each element without the need to modify their code.

This structure allows you to add new operations (new visitors) without modifying the existing element classes, promoting a more flexible and extensible design.
