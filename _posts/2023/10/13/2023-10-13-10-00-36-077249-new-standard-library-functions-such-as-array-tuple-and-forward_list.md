---
layout: post
title: "New standard library functions such as array, tuple, and forward_list"
description: " "
date: 2023-10-13
tags: [References]
comments: true
share: true
---

In modern software development, the C++ programming language continues to evolve and introduce new features. With each iteration, the standard library also expands to provide programmers with more powerful tools.

In this blog post, we will explore some of the new standard library functions that have been introduced to C++ for working with arrays, tuples, and forward lists. These additions aim to simplify and enhance the handling of these widely used data structures.

## 1. Array Functions

### std::size

The `std::size` function returns the number of elements in an array. It provides a convenient way to obtain the size of an array without needing to manually calculate it or rely on the outdated approach of using `sizeof`.

```cpp
#include <array>
#include <iostream>

int main() {
    std::array<int, 5> myArray{1, 2, 3, 4, 5};
    
    int arraySize = std::size(myArray);
    std::cout << "Size of myArray: " << arraySize << std::endl;
    
    return 0;
}
```

Output:
```
Size of myArray: 5
```

### std::empty

The `std::empty` function checks if an array is empty, returning a boolean value indicating whether the array contains any elements or not.

```cpp
#include <array>
#include <iostream>

int main() {
    std::array<int, 0> emptyArray{};
    
    if (std::empty(emptyArray)) {
        std::cout << "The array is empty!" << std::endl;
    } else {
        std::cout << "The array is not empty." << std::endl;
    }
    
    return 0;
}
```

Output:
```
The array is empty!
```

## 2. Tuple Functions

### std::apply

The `std::apply` function applies a callable object (such as a function or lambda) to the elements of a tuple. It unpacks the tuple and passes each element as an argument to the callable object.

```cpp
#include <tuple>
#include <iostream>

void printValues(int a, int b, int c) {
    std::cout << "a: " << a << ", b: " << b << ", c: " << c << std::endl;
}

int main() {
    std::tuple<int, int, int> myTuple{1, 2, 3};
    
    std::apply(printValues, myTuple);
    
    return 0;
}
```

Output:
```
a: 1, b: 2, c: 3
```

### std::make_from_tuple

The `std::make_from_tuple` function constructs an object by forwarding the elements of a tuple as arguments to its constructor. It is particularly useful for creating objects when the types of the constructor arguments are known only at runtime.

```cpp
#include <tuple>
#include <string>
#include <iostream>

class Person {
public:
    Person(const std::string& name, int age) {
        std::cout << "Name: " << name << ", Age: " << age << std::endl;
    }
};

int main() {
    std::tuple<std::string, int> personParams{"John Doe", 25};
    
    std::make_from_tuple<Person>(personParams);
    
    return 0;
}
```

Output:
```
Name: John Doe, Age: 25
```

## 3. Forward List Function

### std::erase_if

The `std::erase_if` function removes elements from a forward list that satisfy a given predicate. It provides a convenient way to remove elements based on a condition without needing to explicitly iterate over the list.

```cpp
#include <forward_list>
#include <iostream>

bool isOdd(int number) {
    return number % 2 != 0;
}

int main() {
    std::forward_list<int> myList{1, 2, 3, 4, 5};
    
    std::erase_if(myList, isOdd);
    
    for (const auto& element : myList) {
        std::cout << element << " ";
    }
    
    return 0;
}
```

Output:
```
2 4
```

## Conclusion

The introduction of these new standard library functions for arrays, tuples, and forward lists simplifies common tasks and allows for more expressive and efficient code. By incorporating these functions into your C++ projects, you can take advantage of the latest language features and improve your development experience.

#References
1. [std::size - C++ Reference](https://en.cppreference.com/w/cpp/iterator/size)
2. [std::empty - C++ Reference](https://en.cppreference.com/w/cpp/iterator/empty)
3. [std::apply - C++ Reference](https://en.cppreference.com/w/cpp/utility/apply)
4. [std::make_from_tuple - C++ Reference](https://en.cppreference.com/w/cpp/utility/make_from_tuple)
5. [std::erase_if - C++ Reference](https://en.cppreference.com/w/cpp/container/forward_list/erase_if)