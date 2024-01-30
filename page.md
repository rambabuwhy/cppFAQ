# Page

## Mutable

In C++, "mutable" is a keyword that is often used in conjunction with member variables of a class. It allows a member variable marked as mutable to be modified even within a const-qualified member function. This is useful when you want to change a member variable's value in a const function without affecting the logical constness of the object.

Here's a simple example to illustrate the use of the `mutable` keyword:

```cpp
cppCopy code#include <iostream>

class MutableExample {
public:
    // Constructor to initialize the mutable variable
    MutableExample(int initialValue) : value(initialValue) {}

    // Const-qualified member function with a mutable member variable
    void printValue() const {
        // Although 'value' is a member variable and this function is const-qualified,
        // we can still modify 'value' because it is marked as mutable.
        value++;
        std::cout << "Current value: " << value << std::endl;
    }

private:
    mutable int value;  // Mutable member variable
};

int main() {
    MutableExample obj(10);
    obj.printValue();  // This will modify 'value' even though printValue is const-qualified

    return 0;
}
```

In this example, the `printValue` member function is marked as `const`, but the `value` member variable is marked as `mutable`. This allows `printValue` to modify the value of `value` even though the function is logically considered const. The use of `mutable` can be helpful in scenarios where you want to update some internal state of an object within a const-qualified member function.
