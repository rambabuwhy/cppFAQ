# Design Pattern-Abstract Factory

The Abstract Factory design pattern is a creational pattern that provides an interface for creating families of related or dependent objects without specifying their concrete classes. This pattern involves defining an interface or abstract class for creating families of related objects, and concrete subclasses or implementations to create the actual objects.

Let's break down the example step by step:

1.  **Define Abstract Products (`AbstractProductA` and `AbstractProductB`):**

    ```cpp
    class AbstractProductA {
    public:
        virtual std::string getName() const = 0;
    };

    class ProductA1 : public AbstractProductA {
    public:
        std::string getName() const override {
            return "Product A1";
        }
    };

    class ProductA2 : public AbstractProductA {
    public:
        std::string getName() const override {
            return "Product A2";
        }
    };

    class AbstractProductB {
    public:
        virtual std::string getName() const = 0;
    };

    class ProductB1 : public AbstractProductB {
    public:
        std::string getName() const override {
            return "Product B1";
        }
    };

    class ProductB2 : public AbstractProductB {
    public:
        std::string getName() const override {
            return "Product B2";
        }
    };
    ```

    Here, we define two families of related products (`ProductA` and `ProductB`). Each product family has an abstract class (`AbstractProductA` and `AbstractProductB`) and concrete implementations (`ProductA1`, `ProductA2`, `ProductB1`, and `ProductB2`).
2.  **Define Abstract Factory (`AbstractFactory`):**

    ```cpp
    class AbstractFactory {
    public:
        virtual AbstractProductA* createProductA() const = 0;
        virtual AbstractProductB* createProductB() const = 0;
    };
    ```

    The `AbstractFactory` declares the creation methods for both `AbstractProductA` and `AbstractProductB`.
3.  **Implement Concrete Factories (`ConcreteFactory1` and `ConcreteFactory2`):**

    ```cpp
    class ConcreteFactory1 : public AbstractFactory {
    public:
        AbstractProductA* createProductA() const override {
            return new ProductA1();
        }

        AbstractProductB* createProductB() const override {
            return new ProductB1();
        }
    };

    class ConcreteFactory2 : public AbstractFactory {
    public:
        AbstractProductA* createProductA() const override {
            return new ProductA2();
        }

        AbstractProductB* createProductB() const override {
            return new ProductB2();
        }
    };
    ```

    The `ConcreteFactory1` and `ConcreteFactory2` classes implement the abstract factory interface by providing specific implementations for creating `ProductA` and `ProductB` objects.
4.  **Client Code (main function):**

    ```cpp
    int main() {
        // Client code using Abstract Factory 1
        AbstractFactory* factory1 = new ConcreteFactory1();
        AbstractProductA* productA1 = factory1->createProductA();
        AbstractProductB* productB1 = factory1->createProductB();

        std::cout << "Product A: " << productA1->getName() << std::endl;
        std::cout << "Product B: " << productB1->getName() << std::endl;

        delete factory1;
        delete productA1;
        delete productB1;

        // Client code using Abstract Factory 2
        AbstractFactory* factory2 = new ConcreteFactory2();
        AbstractProductA* productA2 = factory2->createProductA();
        AbstractProductB* productB2 = factory2->createProductB();

        std::cout << "Product A: " << productA2->getName() << std::endl;
        std::cout << "Product B: " << productB2->getName() << std::endl;

        delete factory2;
        delete productA2;
        delete productB2;

        return 0;
    }
    ```

    In the `main` function, we demonstrate how to use the abstract factories to create products. We create instances of `ConcreteFactory1` and `ConcreteFactory2`, then use them to create instances of `ProductA` and `ProductB`. The client code prints the names of the created products.

    Note: Make sure to handle memory cleanup by deleting dynamically allocated objects.

This example illustrates how the Abstract Factory pattern allows you to create families of related objects without specifying their concrete classes, making it easier to interchange product families.
