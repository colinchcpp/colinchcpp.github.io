---
layout: post
title: "Groovy Compiler-specific extensions"
description: " "
date: 2023-09-23
tags: [groovy, statictyping]
comments: true
share: true
---

Groovy is a powerful and dynamic programming language that runs on the Java Virtual Machine (JVM). It offers numerous features and extensions that make it even more versatile and flexible.

One of the notable features of Groovy is its support for compiler-specific extensions. These extensions provide additional functionality and enhancements that are not available in regular Groovy code. In this blog post, we will explore some of these extensions and how they can be used to enhance your Groovy code.

## @CompileStatic

The `@CompileStatic` annotation is a compiler-specific extension in Groovy that allows you to perform static type checking at compile-time. By adding this annotation to a class or method, the Groovy compiler will enforce strict typing rules, similar to those in statically-typed languages like Java.

```groovy
@CompileStatic
class MyStaticClass {
    static int addNumbers(int a, int b) {
        return a + b
    }
}
```

In the above example, the `addNumbers` method is annotated with `@CompileStatic`, indicating that static type checking should be performed. This means that if you try to pass arguments of the wrong type, the compiler will generate an error. This can help catch type-related bugs early in the development process.

## @TypeChecked

The `@TypeChecked` annotation is another compiler-specific extension in Groovy that enables static type checking, but with a different approach. Unlike `@CompileStatic`, `@TypeChecked` performs type checking dynamically, at runtime.

```groovy
@TypeChecked
class MyTypeCheckedClass {
    static int multiplyNumbers(int a, int b) {
        return a * b
    }
}
```

In the above example, the `multiplyNumbers` method is annotated with `@TypeChecked`. This means that the Groovy compiler will perform type checking dynamically, while the code is executed. If any type-related issues are detected, an exception will be thrown, allowing you to catch it and handle it appropriately.

These two compiler-specific extensions provide different ways to perform static type checking in Groovy. You can choose the approach that best suits your needs based on the desired level of type safety and performance requirements.

#groovy #statictyping