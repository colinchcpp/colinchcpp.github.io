---
layout: post
title: "Right angle brackets for nested template declarations"
description: " "
date: 2023-10-13
tags: [links, templates]
comments: true
share: true
---

In modern C++ programming, it is common to use templates to write generic and reusable code. Templates allow you to write functions or classes that can work with different data types without duplicating the code. However, when using nested template declarations, you may encounter an issue with the use of right angle brackets (`>`). In this blog post, we will discuss this issue and provide solutions to overcome it.

## The Problem

In C++, the right angle brackets (`>`) are used to close template declarations. However, when you have nested template declarations, the compiler may misinterpret the closing angle brackets and result in a compilation error.

```cpp
template<typename T>
class Container {
    // ...
};

template<typename Key, typename Value>
class Map {
    Container<Container<Key>> data; // Compilation error!
};
```

In the above code snippet, we have a `Map` class that has a nested `Container` class as its member. However, when we try to declare `Container<Container<Key>>`, the compiler gets confused with the nested angle brackets and produces a compilation error.

## Solution 1: Space between Angle Brackets

One way to resolve the issue is to add a space between the nested angle brackets. This will help the compiler differentiate between the closing brackets.

```cpp
template<typename T>
class Container {
    // ...
};

template<typename Key, typename Value>
class Map {
    Container< Container<Key> > data; // Compiles successfully
};
```

By adding a space between `Container<Key>` and the closing bracket, the compiler can correctly parse the nested templates.

## Solution 2: Using the `typename` Keyword

Another solution is to use the `typename` keyword before the nested type declaration. This informs the compiler that `Container<Key>` is a type, and not a dependent name.

```cpp
template<typename T>
class Container {
    // ...
};

template<typename Key, typename Value>
class Map {
    typename Container<Container<Key>> data; // Compiles successfully
};
```

By using the `typename` keyword, we help the compiler understand that `Container<Container<Key>>` is a type and not a member variable.

## Conclusion

When using nested template declarations in C++, it is important to be aware of the issue with the right angle brackets (`>`). By adding a space between the brackets or using the `typename` keyword, we can overcome this problem and successfully compile the code.

Remember, understanding these nuances will help you write clean and error-free code when working with templates. Happy coding!

References:
- [C++ Templates - cppreference.com](https://en.cppreference.com/w/cpp/language/templates)
- [Nested templates with the template<> construct](https://stackoverflow.com/questions/10116318/nested-templates-with-the-template-construct)  
- [C++ Gotchas Part 2: Right Angle Brackets](https://devblogs.microsoft.com/cppblog/c-gotchas-right-angle-brackets/)  
- [How stackoverflow’s Markdown is Rendered](https://stackoverflow.com/editing-help#links) 

#cpp #templates