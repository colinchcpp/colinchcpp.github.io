---
layout: post
title: "Reading user input from the console"
description: " "
date: 2023-09-26
tags: []
comments: true
share: true
---

## Python
```python
# Read a single line of input from the console
user_input = input("Enter your name: ")
print("Hello, " + user_input + "!")

# Read multiple inputs on a single line
name, age = input("Enter your name and age: ").split()
print("Your name is " + name + " and you are " + age + " years old.")
```

## JavaScript
```javascript
// Read a single line of input from the console
const readline = require("readline");

const rl = readline.createInterface({
  input: process.stdin,
  output: process.stdout,
});

rl.question("Enter your name: ", (answer) => {
  console.log("Hello, " + answer + "!");
  rl.close();
});

// Read multiple inputs on a single line
rl.question("Enter your name and age: ", (answer) => {
  const [name, age] = answer.split(" ");
  console.log("Your name is " + name + " and you are " + age + " years old.");
  rl.close();
});
```

## Java
```java
import java.util.Scanner;

public class ReadInput {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        // Read a single line of input from the console
        System.out.print("Enter your name: ");
        String name = scanner.nextLine();
        System.out.println("Hello, " + name + "!");

        // Read multiple inputs on a single line
        System.out.print("Enter your name and age: ");
        String[] inputs = scanner.nextLine().split(" ");
        String username = inputs[0];
        int age = Integer.parseInt(inputs[1]);
        System.out.println("Your name is " + username + " and you are " + age + " years old.");
    }
}
```

## C++
```cpp
#include <iostream>
#include <string>

int main() {
    std::string name;
    int age;

    // Read a single line of input from the console
    std::cout << "Enter your name: ";
    std::getline(std::cin, name);
    std::cout << "Hello, " << name << "!" << std::endl;

    // Read multiple inputs on a single line
    std::cout << "Enter your name and age: ";
    std::cin >> name >> age;
    std::cout << "Your name is " << name << " and you are " << age << " years old." << std::endl;

    return 0;
}
```

## Conclusion

Reading user input from the console is a common task in programming. By utilizing the appropriate methods or libraries in each programming language, you can capture user input and use it to enhance the functionality of your applications. 

#programming #console #input