# SOLID-Summary

#### 1. **Single Responsibility Principle (SRP):**

Q: Can you explain the Single Responsibility Principle?

A: The SRP states that a class should have only one reason to change, meaning it should have only one responsibility.

```cpp
// Example:
class FileManager {
public:
    void readFromFile(const std::string& filename);
    void writeToFile(const std::string& filename, const std::string& content);
};
```

#### 2. **Open/Closed Principle (OCP):**

Q: Explain the Open/Closed Principle.

A: The OCP states that a class should be open for extension but closed for modification.

```cpp
// Example:
class Shape {
public:
    virtual double area() const = 0;  // Open for extension
};

class Circle : public Shape {
public:
    double area() const override { /* Calculation for circle area */ }
};
```

#### 3. **Liskov Substitution Principle (LSP):**

Q: What is the Liskov Substitution Principle?

A: The LSP states that objects of a superclass should be replaceable with objects of a subclass without affecting the correctness of the program.

```cpp
// Example:
class Bird {
public:
    virtual void fly() const { /* Implementation for flying */ }
};

class Penguin : public Bird {
public:
    void fly() const override { /* Penguins can't fly */ }
};
```

#### 4. **Interface Segregation Principle (ISP):**

Q: Describe the Interface Segregation Principle.

A: The ISP states that a class should not be forced to implement interfaces it does not use.

```cpp
// Example:
class Worker {
public:
    virtual void work() = 0;
    virtual void eat() = 0;
};

class Robot : public Worker {
public:
    void work() override { /* Implementation for working */ }
    void eat() override {} // Robots don't eat, violates ISP
};
```

#### 5. **Dependency Inversion Principle (DIP):**

Q: What does the Dependency Inversion Principle emphasize?

A: The DIP states that high-level modules should not depend on low-level modules; both should depend on abstractions.

```cpp
// Example:
class LightBulb {
public:
    void turnOn() { /* Implementation for turning on */ }
    void turnOff() { /* Implementation for turning off */ }
};

class Switch {
public:
    virtual void operate(LightBulb& bulb) = 0;  // Abstraction
};

class RemoteControl : public Switch {
public:
    void operate(LightBulb& bulb) override { /* Use remote to operate bulb */ }
};
```

These questions cover the fundamental concepts of SOLID principles in C++. During an interview, it's essential to provide clear explanations and, if possible, discuss practical examples to showcase your understanding.
