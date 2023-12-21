---
title: explicit关键词
date: 2023-12-22 00:23:38
tags: c++
category: c++
---

在 C++ 中，`explicit` 关键字用于防止类构造函数的隐式自动类型转换。默认情况下，如果一个构造函数只接受一个参数（或所有参数都有默认值），它可以被用作隐式类型转换操作符，这意味着它可以在不经过显式转换的情况下将一种类型的值转换为类类型的对象。

使用 `explicit` 关键字可以阻止编译器执行这种隐式转换，这有助于避免意外的类型转换可能导致的错误和混淆。当你希望类构造函数只在明确使用构造语法时被调用时，你应该将它声明为 `explicit`

例如，考虑以下类：

```c++
class MyString {
public:
    MyString(const char* s) {
        // 构造函数，将const char*类型的字符串转换为MyString对象
    }
};
```

<!--more-->

如果没有 `explicit` 关键字，以下代码将被编译器接受，因为它会隐式地使用单参数构造函数将 `const char*` 类型转换为 `MyString` 类类型：

```c++
void printString(const MyString& str) {
    // ...
}

printString("Hello, World!"); // 隐式调用 MyString(const char*) 构造函数
```

为了防止这种隐式转换，你可以使用 `explicit` 关键字：

```c++
class MyString {
public:
    explicit MyString(const char* s) {
        // 构造函数，现在它阻止隐式转换
    }
};

printString("Hello, World!"); // 将产生编译错误
printString(MyString("Hello, World!")); // 正确的显式转换
```

在上面的修正版本中，第一个 `printString` 调用将不会编译通过，因为编译器不再执行隐式的构造函数调用。必须使用显式构造函数调用，如第二个 `printString` 调用所示。

`explicit` 关键字也可以用于 C++11 引入的转换操作符，以防止隐式类型转换。

```c++
class MyString {
public:
    // ...
    explicit operator std::string() const {
        return std::string(/*...*/);
    }
};

MyString myStr(/*...*/);
std::string str = static_cast<std::string>(myStr); // 显式转换
std::string str2 = myStr; // 将产生编译错误，因为转换操作符是 explicit 的
```

在这个例子中，即使 `MyString` 类提供了到 `std::string` 的转换，该转换操作符被声明为 `explicit`，所以它不会执行隐式转换。需要使用显式 `static_cast` 进行转换。
