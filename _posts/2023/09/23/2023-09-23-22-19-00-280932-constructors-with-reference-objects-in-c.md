---
layout: post
title: "Constructors with Reference Objects in C++"
description: " "
date: 2023-09-23
tags: [Cplusplus]
comments: true
share: true
---

Constructors are special member functions used to initialize the objects of a class. In C++, a constructor can also accept reference objects as parameters. This allows you to initialize the member variables of an object with existing objects.

Here's an example of a class with a constructor that accepts a reference object:

```cpp
#include <iostream>

class Rectangle {
   private:
    int length;
    int width;

   public:
    Rectangle(int& len, int& wid) {
        length = len;
        width = wid;
    }

    void display() {
        std::cout << "Length: " << length << std::endl;
        std::cout << "Width: " << width << std::endl;
    }
};

int main() {
    int length = 5;
    int width = 3;

    Rectangle rect(length, width);
    rect.display();

    return 0;
}
```

In the above example, the `Rectangle` class has a constructor that accepts two integer reference parameters: `len` and `wid`. The member variables `length` and `width` of the `Rectangle` object are initialized with the values passed through the constructor.

Inside the `main` function, two integer variables `length` and `width` are declared and initialized with values `5` and `3` respectively. These variables are then used as arguments while creating an instance of the `Rectangle` class. Finally, the `display` method is called to print the length and width of the rectangle object.

By passing objects by reference in the constructor, you can avoid unnecessary object copying and efficiently initialize the member variables using existing objects.

Remember to use appropriate access specifiers and adapt the code as per your requirements.

#Cplusplus #Constructors #ReferenceObjects