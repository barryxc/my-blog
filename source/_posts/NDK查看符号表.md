---
title: NDK查看符号表
date: 2023-03-31 14:24:31
tags:
category:
---



方法一：
```java
nm ${so文件}
```

方法二：
```java
objdump --syms  ${so文件}
```
