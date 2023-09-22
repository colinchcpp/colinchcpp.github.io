---
layout: post
title: "Recursive templates for template aliases in C++"
description: " "
date: 2023-09-22
tags: [templates]
comments: true
share: true
---

When working with templates in C++, it is common to come across situations where you want to define a template alias that depends on another template alias. In C++, this can be achieved using recursive template aliases. Recursive template aliases allow you to define a template alias that refers to itself in its definition, creating a chain of dependencies.

To better understand recursive template aliases, let's go through an example. Suppose we have a template alias called `List`, which represents a list of types:

```cpp
template <typename... Ts>
using List = std::tuple<Ts...>;
```

Now, let's say we want to define another template alias called `NestedList`, which represents a nested list of types. In other words, `NestedList` should be a `List` of `List` of types. Here's how we can achieve this using recursive template aliases:

```cpp
template <typename... Ts>
using NestedList = List<NestedList<Ts>...>;
```

In the above code, the `NestedList` template alias uses itself as one of the template arguments of the `List` template alias. This creates a recursive chain, where each level of nesting refers to the next level of nesting.

We can now use the `NestedList` template alias to define nested lists of types:

```cpp
using MyNestedList = NestedList<int, double, char>;

// MyNestedList is equivalent to List<List<int, double, char>, List<int, double, char>, List<int, double, char>>
```

By using recursive template aliases, we can easily define complex type hierarchies based on other template aliases. This allows for flexible and expressive template metaprogramming, enabling us to create more powerful and generic code.

However, it's important to exercise caution when using recursive template aliases, as they can quickly lead to deep nesting and increased compile times. It's advisable to use them sparingly and make sure to test their impact on compile times in larger projects.

#cpp #templates