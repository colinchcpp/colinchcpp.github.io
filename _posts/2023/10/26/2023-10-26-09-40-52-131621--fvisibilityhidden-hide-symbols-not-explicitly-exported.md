---
layout: post
title: "-fvisibility=hidden (hide symbols not explicitly exported)"
description: " "
date: 2023-10-26
tags: []
comments: true
share: true
---

When developing software applications, it is important to manage symbol visibility to control how functions and variables are accessed by other code modules. By default, all symbols in a compiled program are visible to other modules, which can lead to potential issues like symbol clashes or unintentional usage of internal functions.

To address this concern, the `-fvisibility=hidden` flag is commonly used in programming languages like C and C++. This flag allows developers to hide symbols that are not explicitly exported, preventing them from being accessed outside of their intended scope.

## How to use -fvisibility=hidden

To use `-fvisibility=hidden` and hide symbols not explicitly exported, you need to follow these steps:

1. Open your project's build settings or Makefile.

2. Locate the compiler flags section.

3. Add `-fvisibility=hidden` to the compiler flags. This flag tells the compiler to hide symbols that are not explicitly marked as exported.

4. Recompile your project with the updated compiler flags.

## Benefits of -fvisibility=hidden

Using `-fvisibility=hidden` can offer several benefits:

- **Reduced symbol clashes**: By hiding symbols that are not intended for external use, you minimize the chances of symbol clashes with other libraries or modules.

- **Improved encapsulation**: Keeping internal functions and variables hidden discourages accidental use outside their intended scope, promoting better encapsulation and maintenance of code.

- **Smaller binary size**: Hiding unused symbols can result in smaller binary files since they are not included in the final output.

## Conclusion

The `-fvisibility=hidden` flag is a useful tool for managing symbol visibility in software development. By using this flag, you can hide symbols that are not explicitly exported, reducing symbol clashes, improving encapsulation, and potentially reducing the size of your binary files.