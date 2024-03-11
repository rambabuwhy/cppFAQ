# Design Pattern- Interpreter

The Interpreter design pattern is a behavioral pattern that defines a grammar for the language and provides an interpreter to interpret sentences in that language. It involves defining a language grammar and implementing an interpreter that can parse and interpret sentences in that grammar. This pattern is particularly useful when you have a language to interpret and you want to represent its grammar and provide a way to evaluate expressions in that language.

Let's break down the implementation step by step:

1.  **Expression class:**

    ```cpp
    class Expression {
    public:
        virtual int interpret(std::unordered_map<std::string, int>& context) = 0;
    };
    ```

    Here, `Expression` is an abstract class representing the abstract syntax tree (AST) node. It declares a pure virtual function `interpret`, which concrete subclasses will implement to interpret expressions.
2.  **VariableExpression class:**

    ```cpp
    class VariableExpression : public Expression {
    private:
        std::string variable;

    public:
        VariableExpression(const std::string& var) : variable(var) {}

        int interpret(std::unordered_map<std::string, int>& context) override {
            return context[variable];
        }
    };
    ```

    `VariableExpression` is a terminal expression class. It represents a variable in the language. The `interpret` method returns the value of the variable from the context.
3.  **AddExpression class:**

    ```cpp
    class AddExpression : public Expression {
    private:
        Expression* left;
        Expression* right;

    public:
        AddExpression(Expression* l, Expression* r) : left(l), right(r) {}

        int interpret(std::unordered_map<std::string, int>& context) override {
            return left->interpret(context) + right->interpret(context);
        }
    };
    ```

    `AddExpression` is a non-terminal expression class. It represents an addition operation. The `interpret` method evaluates the left and right expressions and returns their sum.
4.  **Client code:**

    ```cpp
    int main() {
        // Context (variable assignments)
        std::unordered_map<std::string, int> context;
        context["x"] = 5;
        context["y"] = 10;

        // Creating expressions
        Expression* expression = new AddExpression(new VariableExpression("x"), new VariableExpression("y"));

        // Interpreting the expression
        int result = expression->interpret(context);

        // Output the result
        std::cout << "Result: " << result << std::endl;

        // Cleanup
        delete expression;

        return 0;
    }
    ```

    In the `main` function, we create a context with variable assignments ("x" is 5, "y" is 10). Then, we create an expression (`AddExpression`) by combining two variable expressions ("x" and "y"). Finally, we interpret the expression in the given context and output the result.
5.  **Output:**

    ```makefile
    makefileCopy codeResult: 15
    ```

    The result is the sum of the values assigned to "x" and "y" in the context.

This example illustrates the basic structure of the Interpreter pattern. You can extend it to support more complex expressions and operations by adding new classes derived from `Expression`.
