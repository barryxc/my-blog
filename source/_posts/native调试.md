---
title: post
date: 2024-04-06 19:45:40
tags:
category: debug
---

# Native 调试总结

- debug so 才可以调试，release so 不可以调试。
- 还原堆栈需要 /build/intermediates/cmake目录下的 so 才可以
- 使用 sdk 工程调试另外一个 app 时需要修改 sdk工程中的 app 模块的包名和调试的 apk 一致。
- 通过 dlopen() 的 so，默认不执行 jni_onload，只有 java层的 system.loadlibrary()才会执行。想要执行 jni_onload 执行 so 库初始化，需要手动调用 java 层的加载机制。
- dlsym()函数获取符号地址时，要保证 so 的符号被导出。可以通过 nm -D  xx.so 命令查看是否有对应的符号

<!--more-->

- Gcc 编译默认会命名修饰函数符号，所以需要对导出的符号进行 extern C 修饰。
- debug so 默认携带调试信息，不会携带完整的符号信息。
- nm xx.so 命令默认只会输出静态分析的符号，不会输出动态符号。输出动态符号需要 -D 选项。
- DWARF 是一种标准的调试数据格式，用于在可执行文件中存储和描述程序的调试信息。
