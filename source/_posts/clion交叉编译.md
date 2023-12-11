---
title: clion交叉编译
date: 2023-12-12 00:22:27
tags:
category:
---

编译 android 平台产物

![img](https://intranetproxy.alipay.com/skylark/lark/0/2021/png/3756563/1621793280166-b7803ca4-0db1-438e-8523-ee00961efbaa.png)

```plain
-DCMAKE_TOOLCHAIN_FILE=/Users/barry/Library/Android/sdk/ndk/20.0.5594570/build/cmake/android.toolchain.cmake
-DANDROID_ABI=armeabi-v7a
```



**参考文档**

- [Cross Compiling for Android](https://cmake.org/cmake/help/latest/manual/cmake-toolchains.7.html#id22)
- [Cmake交叉编译详解](https://blog.csdn.net/jirryzhang/article/details/72793363)
- [CMake 工具链文件](https://developer.android.com/ndk/guides/cmake#command-line)
