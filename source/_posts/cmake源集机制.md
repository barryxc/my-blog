---
title: cmake源集机制
date: 2021-12-26 17:16:55
tags: cmake
category: cmake
---

[cmake](https://cmake.org/cmake/help/latest/guide/tutorial/index.html)

在 CMake 中，并没有一个默认机制来自动查找源码文件。CMake 需要你在 `CMakeLists.txt` 配置文件中显式地指定源码文件。这意味着 CMake 不会去猜测或自动探测你的源码文件所在；你必须明确告诉 CMake 需要编译哪些文件。

通常，你会在 `CMakeLists.txt` 文件中使用 `add_executable` 或者 `add_library` 命令来定义编译目标，并显式地列出构成该目标的所有源码文件。例如：

```cmake
add_executable(MyExecutable main.cpp foo.cpp bar.cpp)
```

在这个例子中，`MyExecutable` 是目标的名字，`main.cpp`、`foo.cpp` 和 `bar.cpp` 是明确指定的源码文件。

如果你有一组相对固定的源码文件，你可以简单地将它们全部列出。然而，对于较大的项目或者源码文件经常变动的情况，逐一列出所有文件可能会变得繁琐。为了简化这个过程，CMake 提供了一些命令来帮助你查找和指定源码文件，这些命令包括 `aux_source_directory` 和 `file(GLOB ...)`。虽然这些命令可以帮助收集源码文件，但它们通常不是最佳实践，因为它们无法跟踪文件系统中的变化（例如，当你添加或删除文件时，CMake 不会自动更新）。

例如，使用 `file(GLOB ...)` 可以根据模式匹配查找文件：

```cmake
file(GLOB MY_SOURCES "*.cpp") # 不推荐用于源文件
add_executable(MyExecutable ${MY_SOURCES})
```

在这个例子中，`MY_SOURCES` 变量会包含当前目录下所有后缀为 `.cpp` 的源码文件。

总结来说，CMake 需要你在 `CMakeLists.txt` 中显式指定源码文件，它不会默认查找源码文件。你可以使用 `file(GLOB ...)` 或 `aux_source_directory` 这样的命令来收集源码文件，但最好的实践仍然是显式地列出所有源码文件，尤其是对于那些希望确保构建系统适应性和可维护性的项目来说。
