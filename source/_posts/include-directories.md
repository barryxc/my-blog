---
title: include_directories和target_include_directories
date: 2023-12-26 17:52:53
tags: cmake
category: cmake
---

[cmake](https://cmake.org/cmake/help/latest/guide/tutorial/index.html)

`include_directories`是CMake中的一个命令，其作用是向项目中添加包含目录（**即头文件搜索路径**）。当编译器编译项目中的源代码文件时，它会在这些指定的目录中查找`#include`指令引用的头文件。

使用 `include_directories` 命令可以使编译器搜索项目内外的附加目录，从而找到所需的头文件。这对于跨目录的项目结构或者使用第三方库非常有用。

下面是一个`include_directories`的使用示例：

```cmake
include_directories(includes /path/to/external/includes)
```

在这个例子中，`includes`是项目内的一个目录，指的是相对于当前`CMakeLists.txt`文件所在目录的相对路径。`/path/to/external/includes`是系统中某个外部库头文件的绝对路径。这条命令将这两个目录添加到编译器的头文件搜索路径中。

一旦使用了`include_directories`，它会影响所有随后定义的目标（例如使用`add_executable`或者`add_library`定义的可执行文件或库）。如果你希望对特定目标设置包含目录而不影响其他的，应使用`target_include_directories`命令，它提供了更细粒度的控制。

例如：

```cmake
add_executable(MyExecutable main.cpp)
target_include_directories(MyExecutable PRIVATE includes)
```

在这个例子中，`MyExecutable`仅会包含`includes`目录作为私有依赖，这意味着这个包含目录仅对`MyExecutable`可见，不会影响到其他目标。

通常建议使用`target_include_directories`而非`include_directories`，因为前者更符合现代CMake的目标属性设置方式，允许更好的封装性和可重用性
