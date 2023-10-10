---
layout: post
title: "Queue-based approach to evaluate the postfix expression in C++"
description: " "
date: 2023-10-10
tags: []
comments: true
share: true
---

In this article, we will explore a queue-based approach to evaluate a postfix expression in C++. Postfix expressions are mathematical expressions where the operators appear after the operands. For example, the postfix form of the expression "3 + 4" is "3 4 +".

To evaluate a postfix expression, we will use a queue to store the operands and a stack to store the intermediate results.

## Algorithm:

1. Create an empty stack and an empty queue.
2. Read the postfix expression from left to right.
3. If the current element is an operand, enqueue it in the queue.
4. If the current element is an operator, pop two operands from the queue.
5. Apply the operator to the operands and push the result back into the queue.
6. Repeat steps 3 to 5 until the entire expression is scanned.
7. The final result will be the only element remaining in the queue.

## C++ Implementation:

```C++
#include <iostream>
#include <stack>
#include <queue>
#include <string>

using namespace std;

int evaluatePostfix(string expression) {
    stack<int> operandStack;
    queue<int> operandQueue;

    for (char c : expression) {
        if (isdigit(c)) {
            operandQueue.push(c - '0');
        } else if (c != ' ') {
            int operand2 = operandQueue.front();
            operandQueue.pop();
            int operand1 = operandQueue.front();
            operandQueue.pop();
            
            switch (c) {
                case '+':
                    operandQueue.push(operand1 + operand2);
                    break;
                case '-':
                    operandQueue.push(operand1 - operand2);
                    break;
                case '*':
                    operandQueue.push(operand1 * operand2);
                    break;
                case '/':
                    operandQueue.push(operand1 / operand2);
                    break;
            }
        }
    }

    return operandQueue.front();
}

int main() {
    string postfixExpression = "3 4 +";
    int result = evaluatePostfix(postfixExpression);

    cout << "Result: " << result << endl;

    return 0;
}
```

## Example Run:

### Input:
Postfix Expression: "3 4 +"

### Output:
Result: 7

By using this queue-based approach, we can easily evaluate postfix expressions in C++. This method allows for efficient processing of postfix expressions with minimal memory overhead.