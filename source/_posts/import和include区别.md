---
title: import和include区别
date: 2021-12-18 21:32:15
tags: c++
category: c++ 
---

在Java和C++中，包含和访问库中的类型（如字符串）有不同的机制。

### Java中的`import`语句：

在Java中，当你使用`import`语句时，**它告诉编译器在编译时需要查找哪些类**。Java中的`String`类位于`java.lang`包中，该包是自动被所有Java程序导入的，因此你通常不需要显式导入`java.lang.String`。你可以直接使用`String`类而不需要任何前缀。

```java
import java.util.List; // 导入java.util包中的List接口

public class MyClass {
    public static void main(String[] args) {
        String myString = "Hello, World!"; // 直接使用String
        List<String> myList; // 使用导入的List接口
    }
}
```

### C++中的`#include`指令：

在C++中，当你使用`#include <string>`预处理指令时，**你是在告诉编译器在编译之前将`<string>`头文件的内容文本替换到源文件中**。然而，C++标准库中的很多功能都是在命名空间`std`中定义的。

因此，当你包含`<string>`头文件后，你还需要使用`std::`的前缀来访问`std`命名空间中的`string`类。

<!--more-->

```c++
#include <string>
#include <vector>

int main() {
    std::string myString = "Hello, World!"; // 使用std命名空间的前缀
    std::vector<int> myVector; // 同样使用std命名空间的前缀
}

```

如果你想避免在每次使用标准库中的类型时都键入`std::`前缀，你可以使用`using`声明或`using`指令。但请注意，过度使用`using namespace std;`可能会导致名称冲突，特别是在大型项目或头文件中。

```c++
#include <string>
#include <vector>

using std::string; // 只导入std命名空间中的string类
using std::vector; // 只导入std命名空间中的vector类

int main() {
    string myString = "Hello, World!"; // 不需要std::前缀
    vector<int> myVector; // 不需要std::前缀
}
```

或者：

```c++
#include <string>
#include <vector>

using namespace std; // 导入整个std命名空间

int main() {
    string myString = "Hello, World!"; // 不需要std::前缀
    vector<int> myVector; // 不需要std::前缀
}
```

总结来说，C++中的`#include <string>`和Java中的`import java.lang.String`有不同的含义和行为。在C++中，即使包含了`<string>`头文件，也需要指定命名空间前缀`std::`来访问`string`类，除非你使用了`using`声明或指令来引入`std`命名空间。
