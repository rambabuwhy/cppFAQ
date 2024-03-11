# Design Pattern-Factory Method

The Factory Method is a creational design pattern that provides an interface for creating objects in a superclass but allows subclasses to alter the type of objects that will be created. This pattern promotes loose coupling between the client code and the created objects.

Let's break down the example step by step:

#### Step 1: Define the Abstract Product

```cpp
// Abstract Product
class Product {
public:
    virtual ~Product() = default;
    virtual std::string getName() const = 0;
};
```

Here, `Product` is an abstract class defining the interface for concrete products. In this case, it has a pure virtual function `getName()`.

#### Step 2: Implement Concrete Products

```cpp
// Concrete Product A
class ConcreteProductA : public Product {
public:
    std::string getName() const override {
        return "ConcreteProductA";
    }
};

// Concrete Product B
class ConcreteProductB : public Product {
public:
    std::string getName() const override {
        return "ConcreteProductB";
    }
};
```

Two concrete classes (`ConcreteProductA` and `ConcreteProductB`) implement the `Product` interface. Each concrete product provides its own implementation of the `getName()` function.

#### Step 3: Define the Abstract Creator

```cpp
// Abstract Creator
class Creator {
public:
    virtual ~Creator() = default;
    virtual Product* createProduct() const = 0;
    
    void anOperation() const {
        // Some common operation
        std::cout << "Performing common operation in Creator." << std::endl;
        
        // Use the factory method to create a product
        Product* product = createProduct();
        
        // Use the created product
        std::cout << "Created product: " << product->getName() << std::endl;
    }
};
```

The `Creator` class is an abstract class that declares a pure virtual function `createProduct()`, which acts as the factory method. It also has a common operation (`anOperation()`) that can use the created product.

#### Step 4: Implement Concrete Creators

```cpp
// Concrete Creator A
class ConcreteCreatorA : public Creator {
public:
    Product* createProduct() const override {
        return new ConcreteProductA();
    }
};

// Concrete Creator B
class ConcreteCreatorB : public Creator {
public:
    Product* createProduct() const override {
        return new ConcreteProductB();
    }
};
```

Two concrete creator classes (`ConcreteCreatorA` and `ConcreteCreatorB`) extend the `Creator` class and provide their own implementations of the `createProduct()` factory method.

#### Step 5: Client Code

```cpp
int main() {
    // Client code using Creator A
    Creator* creatorA = new ConcreteCreatorA();
    creatorA->anOperation();
    
    // Client code using Creator B
    Creator* creatorB = new ConcreteCreatorB();
    creatorB->anOperation();
    
    // Cleanup
    delete creatorA;
    delete creatorB;

    return 0;
}
```

In the client code, instances of concrete creators (`ConcreteCreatorA` and `ConcreteCreatorB`) are created. They call the `anOperation()` method, which internally calls the factory method `createProduct()` to create specific products (`ConcreteProductA` and `ConcreteProductB`). The client code remains unaware of the specific product classes being instantiated.

#### Output

The output of the program will be:

```yaml
Performing common operation in Creator.
Created product: ConcreteProductA
Performing common operation in Creator.
Created product: ConcreteProductB
```

This demonstrates the flexibility of the Factory Method pattern, allowing you to create different products with minimal changes to the client code.
