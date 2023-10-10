---
layout: post
title: "Implementing a queue-based infix to postfix conversion in C++"
description: " "
date: 2023-10-10
tags: [programming]
comments: true
share: true
---

Infix expressions are the conventional mathematical expressions we use, for example, `(2 + 3) * 4`, where the operators are written between the operands. On the other hand, postfix expressions have the operators after their operands, such as `2 3 + 4 *`. 

Converting an infix expression to postfix can be useful for various purposes, such as evaluating arithmetic expressions. In this article, we will implement a queue-based infix to postfix conversion algorithm in C++.

## The Algorithm

The algorithm uses a stack and a queue to convert infix expressions to postfix expressions. The stack holds operators, and the queue holds the postfix expression as it is being built. 

The algorithm processes the input infix expression character by character, and when it encounters an operand (a number or a variable), it directly adds it to the output queue. If it encounters an operator, it compares its precedence with the operators present at the top of the stack.

If the operator has higher precedence or the stack is empty, it is pushed onto the stack. If the operator has lower or equal precedence, all the operators with higher precedence from the stack are popped and added to the output queue. Then, the new operator is pushed onto the stack.

Once the input expression is processed, any remaining operators in the stack are popped and added to the output queue. The resulting queue will contain the postfix expression equivalent to the input infix expression.

## Implementation in C++

```cpp
#include <iostream>
#include <stack>
#include <queue>
#include <string>

using namespace std;

// Function to check if a character is an operator
bool isOperator(char c) {
    return (c == '+' || c == '-' || c == '*' || c == '/');
}

// Function to check if a character is an operand
bool isOperand(char c) {
    return (c >= '0' && c <= '9');
}

// Function to get the precedence of an operator
int getPrecedence(char c) {
    if (c == '+' || c == '-')
        return 1;
    else if (c == '*' || c == '/')
        return 2;
    else
        return 0; // Lower precedence for parentheses
}

// Function to convert infix expression to postfix expression
queue<char> infixToPostfix(string infix) {
    stack<char> operatorStack;
    queue<char> postfixQueue;

    for (char c : infix) {
        if (isOperand(c)) {
            postfixQueue.push(c);
        }
        else if (isOperator(c)) {
            while (!operatorStack.empty() && getPrecedence(c) <= getPrecedence(operatorStack.top())) {
                postfixQueue.push(operatorStack.top());
                operatorStack.pop();
            }
            operatorStack.push(c);
        }
        else if (c == '(') {
            operatorStack.push(c);
        }
        else if (c == ')') {
            while (!operatorStack.empty() && operatorStack.top() != '(') {
                postfixQueue.push(operatorStack.top());
                operatorStack.pop();
            }
            operatorStack.pop(); // Pop the opening parenthesis
        }
    }

    while (!operatorStack.empty()) {
        postfixQueue.push(operatorStack.top());
        operatorStack.pop();
    }

    return postfixQueue;
}

int main() {
    string infixExpression = "(2 + 3) * 4";
    queue<char> postfixExpression = infixToPostfix(infixExpression);

    cout << "Infix Expression: " << infixExpression << endl;
    cout << "Postfix Expression: ";
    while (!postfixExpression.empty()) {
        cout << postfixExpression.front() << " ";
        postfixExpression.pop();
    }

    return 0;
}
```

## Conclusion

In this article, we implemented a queue-based algorithm to convert infix expressions to postfix expressions in C++. This conversion process can be useful for evaluating arithmetic expressions or for further processing in other applications. Understanding these algorithms helps in building more complex calculations and mathematical operations within our programs.

If you have any questions or suggestions, please feel free to leave a comment below!

**#programming #c++**