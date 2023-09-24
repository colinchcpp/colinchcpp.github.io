---
layout: post
title: "Microchip MPLAB XC16 C++ Compiler-specific extensions"
description: " "
date: 2023-09-23
tags: [pragma, pragma]
comments: true
share: true
---

The Microchip MPLAB XC16 C++ compiler provides several extensions that are specific to the Microchip PIC microcontrollers. These extensions enhance the capabilities of the C++ language and allow for more efficient code generation. In this blog post, we will explore some of these extensions and how they can be used in your projects.

## #pragma interrupt

The `#pragma interrupt` directive is used to define interrupt service routines (ISRs) in C++. When a specific interrupt occurs, the corresponding ISR is executed. The `#pragma interrupt` directive can be used to declare ISRs with a specific priority, nestability, and vector number.

```c++
#pragma interruptlow MyLowPriISR
void MyLowPriISR()
{
    // Code for low priority ISR
}

#pragma interrupt MyHighPriISR
void MyHighPriISR()
{
    // Code for high priority ISR
}
```

## #pragma config

The `#pragma config` directive is used to specify device configuration settings. These settings are often used to configure the behavior of the microcontroller, such as oscillator selection, watchdog timer configuration, and I/O port settings.

```c++
#pragma config FOSC = INTOSC // Internal oscillator
#pragma config WDTE = OFF // Disable watchdog timer
#pragma config LVP = OFF // Disable low-voltage programming
```

## _ _attribute_ _

The `_ _attribute_ _` keyword is a Microchip-specific extension that allows you to specify special attributes for functions and variables. These attributes can be used to control the placement of code and data in memory, optimize code execution, and specify interrupt-specific attributes.

```c++
void __attribute__((interrupt, auto_psv)) MyISR()
{
    // Code for ISR
}

int __attribute__((section(".my_section"))) myVariable;
```

## Conclusion

These are just a few examples of the Microchip MPLAB XC16 C++ compiler-specific extensions. By leveraging these extensions, you can optimize your code for Microchip PIC microcontrollers and take full advantage of their capabilities. Make sure to consult the compiler documentation for a complete list of available extensions and their usage.

Remember to use the hashtags #Cplusplus and #MicrochipPIC at the end of the blog post to help increase its visibility and reach.