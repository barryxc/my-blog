---
title: typedef用法
date: 2021-08-01 21:56:31
tags: c++
category: c++
---

`typedef`是C和C++中的一个关键字，它用于给数据类型创建一个新的名称（别名）。通过`typedef`，你可以为复杂的数据类型定义一个易于记忆和使用的名称。这在处理结构体、联合体、函数指针等复杂类型时特别有用。

### 基本用法

```c++
typedef existing_type new_type_name;
```

### 示例

#### 1. 为基本数据类型定义别名

```c++
typedef unsigned long ulong;
typedef double real;

ulong number = 123456789;
real pi = 3.14159;
```

<!--more-->

#### 2. 为结构体定义别名

```c++
typedef struct {
    int x;
    int y;
} Point;

Point p1, p2;
p1.x = 10;
p1.y = 20;
```

#### 3. 为指针类型定义别名

```c++
typedef char* string;

string name = "John Doe";
```

#### 4. 为数组类型定义别名

```c++
typedef int Matrix[10][10];

Matrix m;
m[0][0] = 1;
```

#### 5. 为函数指针定义别名

```c++
typedef void (*FunctionPointer)(int, double);

void someFunction(int i, double d) {
    // ...
}

FunctionPointer fp = someFunction;
fp(5, 3.14);
```

#### 6. 为模板类型定义别名（C++11中称为别名模板 `using`）

```c++
#include <vector>
#include <string>

// 使用typedef定义别名
typedef std::vector<std::string> StringVector;

// 使用C++11的using关键字定义别名
using StringVector = std::vector<std::string>;

StringVector names;
names.push_back("Alice");
names.push_back("Bob");
```

### 使用场景

- **提高代码可读性**：`typedef`可以用来简化复杂类型的名称，使代码更易读。
- **平台独立性**：通过`typedef`定义平台相关的类型，可以让代码更容易移植。例如，在不同的系统上，`typedef`可以用来为特定长度的整数类型定义一个统一的名称。
- **抽象层**：`typedef`可以为具体的类型提供一个抽象的层次，使得在代码中更改这个类型时更加容易。
- **API设计**：库或API设计者可以使用`typedef`来确保用户对于API使用的内部类型有一个简洁清晰的视图。

虽然`typedef`在C++中仍然是有效的，但是自C++11起，`using`关键字的别名声明提供了一个更具表达力的替代方案。这在模板编程中尤其有用，因为它允许别名模板的使用。在某些复杂的类型别名情况下，`using`声明比`typedef`更为灵活和清晰。
