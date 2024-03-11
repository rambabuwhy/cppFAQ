# Design Pattern-Memento

The Memento design pattern is a behavioral pattern that provides the ability to restore an object to its previous state. It is often used to implement undo mechanisms in applications. The pattern involves three main roles: the Originator (the object whose state needs to be saved), the Memento (an object that stores the state of the Originator), and the Caretaker (an object that keeps track of the various states of the Originator).

Let's break down the Memento design pattern example step by step:

#### 1. Define the Memento Class:

```cpp
class Memento {
public:
    Memento(const std::string& state) : state_(state) {}

    std::string getState() const {
        return state_;
    }

private:
    std::string state_;
};
```

Here, the `Memento` class represents the object that stores the state of the `Originator`. It has a constructor to initialize the state and a method (`getState()`) to retrieve the state.

#### 2. Define the Originator Class:

```cpp
class Originator {
public:
    void setState(const std::string& state) {
        state_ = state;
        std::cout << "State set to: " << state << std::endl;
    }

    Memento createMemento() {
        std::cout << "Creating Memento..." << std::endl;
        return Memento(state_);
    }

    void restoreMemento(const Memento& memento) {
        state_ = memento.getState();
        std::cout << "Restoring state to: " << state_ << std::endl;
    }

private:
    std::string state_;
};
```

The `Originator` class is the object whose state needs to be saved and restored. It has a method (`setState()`) to set its state, a method (`createMemento()`) to create a Memento object representing its current state, and a method (`restoreMemento()`) to restore its state from a given Memento.

#### 3. Define the Caretaker Class:

```cpp
class Caretaker {
public:
    void addMemento(const Memento& memento) {
        mementos_.push_back(memento);
    }

    Memento getMemento(int index) const {
        if (index >= 0 && index < mementos_.size()) {
            return mementos_[index];
        }
        // Return an empty Memento if the index is out of bounds
        return Memento("");
    }

private:
    std::vector<Memento> mementos_;
};
```

The `Caretaker` class manages a collection of Mementos. It has methods to add a Memento (`addMemento()`) and retrieve a Memento at a specific index (`getMemento()`).

#### 4. Main Function:

```cpp
int main() {
    // Create an Originator
    Originator originator;

    // Create a Caretaker
    Caretaker caretaker;

    // Set the initial state and save the Memento
    originator.setState("State 1");
    caretaker.addMemento(originator.createMemento());

    // Change the state and save the Memento
    originator.setState("State 2");
    caretaker.addMemento(originator.createMemento());

    // Restore to the first state
    originator.restoreMemento(caretaker.getMemento(0));

    return 0;
}
```

In the `main()` function:

* An `Originator` object (`originator`) is created.
* A `Caretaker` object (`caretaker`) is created.
* The initial state of the `Originator` is set to "State 1", and a Memento is created and added to the `Caretaker`.
* The state of the `Originator` is changed to "State 2", and another Memento is created and added to the `Caretaker`.
* Finally, the `Originator` restores its state to the first saved state using the Memento at index 0 in the `Caretaker`.

As a result, the program demonstrates the basic functionality of the Memento pattern, allowing the restoration of an object's previous state.
