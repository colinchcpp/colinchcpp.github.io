---
layout: post
title: "An overview of C++ Modules support in different package managers: Conan, vcpkg, and Biicode"
description: " "
date: 2023-09-15
tags: [cplusplusmodules, packagemanagers]
comments: true
share: true
---

C++ Modules, introduced in C++20, are a revolutionary feature that simplifies the organization and management of C++ code. They allow for improved build times, better encapsulation, and more efficient code reuse. However, with the introduction of C++ Modules, package managers had to adapt to accommodate this new way of managing dependencies. In this article, we will take a look at the support for C++ Modules in three popular package managers: Conan, vcpkg, and Biicode.

## 1. Conan

![conan](https://example.com/conan_logo.png)

Conan, a powerful cross-platform package manager, has been quick to embrace C++ Modules. It provides seamless support for managing and distributing modules within C++ packages. With Conan, developers can easily define C++ Modules as dependencies in their project's `conanfile.txt` or `conanfile.py` files.

To add a C++ Module dependency in Conan, simply specify it in the `requires` section of the `conanfile`:

```cpp
[requires]
my_module/1.0.0
```

Conan takes care of resolving and downloading the necessary module files, ensuring that the project builds successfully. The modules can then be imported in the code using the standard module import syntax.

## 2. vcpkg

![vcpkg](https://example.com/vcpkg_logo.png)

vcpkg, a popular package manager for C++ libraries, has also embraced C++ Modules and offers support for managing them seamlessly. Developers can specify C++ Modules as dependencies in their vcpkg manifest files (`manifest.json`).

To add a C++ Module dependency in vcpkg, simply add it to the `dependencies` section of the manifest file:

```cpp
"dependencies": [
    {
        "name": "my_module",
        "version-string": "1.0.0"
    }
]
```

vcpkg fetches and installs the required module files, ensuring that they are available for the project to use. Developers can then import the modules using the standard import syntax.

## 3. Biicode

![biicode](https://example.com/biicode_logo.png)

Biicode, a C++ dependency manager with a focus on simplicity, also offers support for managing C++ Modules. Developers can declare and manage dependencies on modules in the `biicode.conf` file.

To add a C++ Module dependency in Biicode, simply add it to the `dependencies` section of the `biicode.conf`:

```cpp
[dependencies]
my_module@1.0.0
```

Biicode automatically downloads and includes the required module files, ensuring that they are available during the build process. Developers can then import the modules using the standard import syntax.

## Conclusion

C++ Modules have revolutionized the way C++ code is organized and managed. Thankfully, package managers like Conan, vcpkg, and Biicode have adapted to support this new paradigm. Developers can now easily manage C++ Module dependencies in their projects, ensuring smooth integration and efficient code reuse.

#cplusplusmodules #packagemanagers