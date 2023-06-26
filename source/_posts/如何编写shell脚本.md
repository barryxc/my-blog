---
title: 如何编写shell脚本
date: 2023-06-21 18:06:43
tags: 
- shellcheck
- sublime
category: shell
---


### 如何编写 shell  脚本?

* [升级bash](https://itnext.io/upgrading-bash-on-macos-7138bd1066ba)
* 选择编辑器
* 安装 shell check 语法检查工具

#### 安装 shellcheck 工具

```shell
brew install shellcheck
```

<!--more-->

#### 安装 sublimelinter 插件

```text
sublime text -> preferences -> package control -> install package -> sublimelinter
```

#### 安装 sublimelinter-shellcheck 插件

```text
sublime text -> preferences -> package control -> install package -> sublimelinter-shellcheck
```

#### 查看本地是否安装了插件

```text
sublime text -> preferences -> package control -> list packages -> sublimelinter-shellcheck
```

#### 创建 .sh 脚本

```shell
touch $script.sh 
```

#### 打开文件编辑

```shell
open $script -a Sublime\ Text 
```

#### 语法检查

* 使用 shellcheck 直接语法检查

```shell
shellcheck $script
```

* sublime 插件自动提示

  ![image-20230621181544039](https://p.ipic.vip/r5wmbd.png)
