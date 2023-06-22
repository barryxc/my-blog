---
title: source 命令详解
date: 2023-06-15 16:47:25
tags: source
category: shell
---

## 作用

- `source`命令也称为**点命令**，也就是一个点符号`.`是`bash`的内部命令。 功能：使 `shell `读入指定的`shell`程序文件并依次执行文件中的所有语句。 使用范例：`source $filename `
- 为什么在修改了环境变量后执行`source`命令? 例如当我修改了`/etc/profile`文件，我想让它立刻生效，而不用重新登录；这时就想到用 `source` 命令，如 `source /etc/profile`。这样就重新执行刚修改的初始化文件，使之立即生效。

<!-- more -->

## 区别

`source $filename` 与 `sh $filename` 及 `./$filename` 执行脚本的区别？

- 当`shell`脚本具有可执行权限时，用`sh $filename`与`./filename`执行脚本是没有区别得。`./filename`是因为当前目录没有在`PATH`中，所有`.`是用来表示当前目录的。
- `sh $filename` 重新建立一个**子`shell`**，在子`shell`中执行脚本里面的语句，**该子`shell`继承父`shell`的环境变量，但子`shell`新建的、改变的变量不会被带回父`shell`，除非使用`export`。
- `source $filename`：这个命令其实只是简单地**读取**脚本里面的语句依次在当前`shell`里面**执行**，没有建立新的子`shell`。那么脚本里面所有新建、改变变量的语句都会保存在当前`shell`里面，当这个`shell`关闭后就失效了。