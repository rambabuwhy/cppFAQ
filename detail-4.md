# Detail - 4

The "Rule of Five" in C++ is a set of guidelines related to resource management in classes. It suggests that if a class needs to define or disable any one of the following five special member functions, then it likely needs to define or disable all of them. The five special member functions are:

1. Destructor (`~ClassName()`): Responsible for releasing resources when an object goes out of scope or is explicitly deleted.
2. Copy Constructor (`ClassName(const ClassName&)`): Creates a new object by copying the content of an existing object.
3. Copy Assignment Operator (`ClassName& operator=(const ClassName&)`): Assigns the content of one object to another existing object.
4. Move Constructor (`ClassName(ClassName&&) noexcept`): Creates a new object by moving the content of an existing object.
5. Move Assignment Operator (`ClassName& operator=(ClassName&&) noexcept`): Assigns the content of one object to another by moving resources.

Here's a simple example to illustrate the Rule of Five:

```cpp
#include <iostream>
#include <cstring>

class RuleOfFiveExample {
private:
    char* data;

public:
    // Constructor
    RuleOfFiveExample(const char* str) {
        data = new char[strlen(str) + 1];
        strcpy(data, str);
    }

    // Destructor
    ~RuleOfFiveExample() {
        delete[] data;
    }

    // Copy Constructor
    RuleOfFiveExample(const RuleOfFiveExample& other) {
        data = new char[strlen(other.data) + 1];
        strcpy(data, other.data);
    }

    // Copy Assignment Operator
    RuleOfFiveExample& operator=(const RuleOfFiveExample& other) {
        if (this != &other) {
            delete[] data;
            data = new char[strlen(other.data) + 1];
            strcpy(data, other.data);
        }
        return *this;
    }

    // Move Constructor
    RuleOfFiveExample(RuleOfFiveExample&& other) noexcept {
        data = other.data;
        other.data = nullptr;
    }

    // Move Assignment Operator
    RuleOfFiveExample& operator=(RuleOfFiveExample&& other) noexcept {
        if (this != &other) {
            delete[] data;
            data = other.data;
            other.data = nullptr;
        }
        return *this;
    }

    // Function to display the data
    void displayData() {
        std::cout << "Data: " << data << std::endl;
    }
};

int main() {
    RuleOfFiveExample obj1("Hello");

    // Copy constructor
    RuleOfFiveExample obj2 = obj1;
    obj2.displayData();

    // Move constructor
    RuleOfFiveExample obj3 = std::move(obj1);
    obj3.displayData();

    // Copy assignment operator
    RuleOfFiveExample obj4("World");
    obj4 = obj2;
    obj4.displayData();

    // Move assignment operator
    obj4 = RuleOfFiveExample("New");
    obj4.displayData();

    return 0;
}
```

In this example, the class `RuleOfFiveExample` manages dynamic memory for a character array (`data`). The Rule of Five is followed by providing the necessary implementations for the constructor, destructor, copy constructor, copy assignment operator, move constructor, and move assignment operator.
