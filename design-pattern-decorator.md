# Design Pattern-Decorator

In object-oriented design, the decorator pattern is a structural pattern that allows behavior to be added to an individual object, either statically or dynamically, without affecting the behavior of other objects from the same class. This pattern is achieved by creating a set of decorator classes that are used to wrap concrete components.

Let's break down the decorator pattern example step by step:

1.  **Component Interface (`Coffee`):**

    * `Coffee` is an abstract class that defines the interface for coffee objects.
    * It has a pure virtual function `brew()` that needs to be implemented by concrete components.

    ```cpp
    class Coffee {
    public:
        virtual ~Coffee() = default;
        virtual void brew() const = 0;
    };
    ```
2.  **Concrete Component (`SimpleCoffee`):**

    * `SimpleCoffee` is a concrete class that implements the `Coffee` interface.
    * It represents a basic coffee without any additional decorations.

    ```cpp
    class SimpleCoffee : public Coffee {
    public:
        void brew() const override {
            std::cout << "Brewing a simple coffee." << std::endl;
        }
    };
    ```
3.  **Decorator Base Class (`CoffeeDecorator`):**

    * `CoffeeDecorator` is an abstract class that extends the `Coffee` interface.
    * It contains a pointer to a `Coffee` object, which is the component being decorated.
    * It delegates the `brew()` function to the wrapped `Coffee` object.

    ```cpp
    class CoffeeDecorator : public Coffee {
    protected:
        std::unique_ptr<Coffee> coffee;

    public:
        CoffeeDecorator(std::unique_ptr<Coffee> coffee) : coffee(std::move(coffee)) {}

        void brew() const override {
            if (coffee) {
                coffee->brew();
            }
        }
    };
    ```
4.  **Concrete Decorator (`MilkDecorator` and `SugarDecorator`):**

    * `MilkDecorator` and `SugarDecorator` are concrete classes that extend `CoffeeDecorator`.
    * They add specific behavior to the coffee by extending the `brew()` function.

    ```cpp
    class MilkDecorator : public CoffeeDecorator {
    public:
        MilkDecorator(std::unique_ptr<Coffee> coffee) : CoffeeDecorator(std::move(coffee)) {}

        void brew() const override {
            CoffeeDecorator::brew();
            addMilk();
        }

    private:
        void addMilk() const {
            std::cout << "Adding milk to the coffee." << std::endl;
        }
    };

    class SugarDecorator : public CoffeeDecorator {
    public:
        SugarDecorator(std::unique_ptr<Coffee> coffee) : CoffeeDecorator(std::move(coffee)) {}

        void brew() const override {
            CoffeeDecorator::brew();
            addSugar();
        }

    private:
        void addSugar() const {
            std::cout << "Adding sugar to the coffee." << std::endl;
        }
    };
    ```
5.  **Client Code (`main` function):**

    * In the `main` function, we create a `SimpleCoffee` object and brew it.
    * Then, we decorate the `SimpleCoffee` with `MilkDecorator` and `SugarDecorator` in a specific order to create a more complex coffee.
    * Finally, we brew the decorated coffee.

    ```cpp
    int main() {
        // Creating a simple coffee
        std::unique_ptr<Coffee> simpleCoffee = std::make_unique<SimpleCoffee>();
        simpleCoffee->brew();

        std::cout << "\n";

        // Decorating the simple coffee with milk and sugar
        std::unique_ptr<Coffee> milkAndSugarCoffee = std::make_unique<MilkDecorator>(
            std::make_unique<SugarDecorator>(std::move(simpleCoffee))
        );

        milkAndSugarCoffee->brew();

        return 0;
    }
    ```

When you run this program, you'll see the following output:

```css
Brewing a simple coffee.

Brewing a simple coffee.
Adding sugar to the coffee.
Adding milk to the coffee.
```

This demonstrates how the decorator pattern allows you to dynamically add or modify behavior of objects at runtime by combining different decorators. In this case, the `MilkDecorator` and `SugarDecorator` are used to enhance a basic coffee object.
