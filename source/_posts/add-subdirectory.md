---
title: add_subdirectory
date: 2021-12-26 17:50:08
tags: cmake
category: cmake
---

[cmake](https://cmake.org/cmake/help/latest/guide/tutorial/index.html)

在 Java 中，"submodule" 这个术语并不是官方的编程概念，而是通常用于描述较大项目中的组织结构，尤其是在使用 Maven 或 Gradle 这样的构建工具时。这些构建工具允许你创建多模块（multi-module）项目，其中每个模块可以有自己的构建生命周期和依赖管理。

如果将 CMake 中的 `add_subdirectory` 命令与 Java 多模块项目的概念进行比较，那么可以说它们在概念上是相似的。`add_subdirectory` 允许你将一个目录（可以认为是一个模块或子项目）添加到主项目的构建过程中。这个目录通常包含它自己的 `CMakeLists.txt` 文件，定义了如何构建该目录中的代码。

在 Java 的多模块项目中，每个模块也会有自己的构建配置文件（例如 Maven 的 `pom.xml`），定义了模块的构建过程和依赖。

例如，在 Maven 中，你的项目结构可能如下：

```
project/
│
├── pom.xml                 # 父项目的 Maven POM 文件
│
├── submodule1/
│   └── pom.xml             # 子模块的 Maven POM 文件
│
└── ...
```

父项目的 `pom.xml` 文件会包含对所有子模块的引用：

```xml
<modules>
    <module>submodule1</module>
    <module>submodule2</module>
    <!-- ... -->
</modules>
```

将 Maven 的多模块项目和 CMake 中的 `add_subdirectory` 命令进行类比，它们都有以下相似之处：

- 都是将一个较大的项目组织为更小、更易管理的组件或模块。
- 每个模块或组件都有自己的构建配置和构建过程。
- 主项目配置文件包含对这些子模块或组件的引用，并且管理整个构建过程。

总之，尽管 CMake 和 Java 构建工具（如 Maven 或 Gradle）在技术细节上不同，`add_subdirectory` 与 Java 多模块项目的概念在组织和管理大型代码基础方面确实有一定的相似性。
