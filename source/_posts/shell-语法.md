---
title: shell 语法
date: 2022-04-28 00:13:48
tags: shell
category: shell
---

## 变量声明

```shell
a="2"
```

## 读取键盘输入

```shell
# \当做普通字符
read -r "please input your name~ "
```

## 转义字符

```shell
\
```

<!-- more -->

## 切换 shell

```shell
chsh -s /bin/bash
```

## 切换目录

```shell
cd
```

## 拷贝

```shell
cp
```

## 创建文件

```shell
touch
```

## 移动&重命名

```shell
mv
```

## 打开文件或文件夹

```shell
open
```

## 查看文件内容

```shell
cat
```

## 查看文件类型

```shell
file
```

## 列表

```shell
# -long format
ls -al
```

## 创建文件夹

```shell
mkdir
```

## 删除文件或文件夹

```shell
rm
rmdir
```

## #打开 vi 程序编辑器

```shell
vim
```

## 查看命令

```shell
type
```

## 正则匹配

```shell
grep
```

## 修改权限

```shell
chmod a+x file
#修改用户
chown
#修改用户组
chgrp
```

## 查找文件

```shell
find
```

## 打印当前目录

```shell
pwd
```

## 执行脚本

```shell
sh #开启子shell进程执行脚本
source #当前shell执行脚本
. #执行脚本
```

## 结束命令

```shell
^C #终止命令
^Z #暂停命令
```

## 别名

```shell
alias #查看所有别名&设置别名
```

## 输出

```shell
echo
```

## 清空屏幕

```shell
clear
```

## 优先执行子命令

```shell
$() #优先执行子命令
` ` #优先执行子命令
```

## 查看所有环境变量

```shell
env
```

## 查询命令手册

```
man ${cmd}
```

## 其它

```shell
export #导出变量使得变量成为环境变量，下次启动无效
$? #上个命令回传码
$0 #执行脚本文件名
uname #获取操作系统名称
basename # 获取基本文件名
dirname #获取父路径
ifconfig #获取ip地址
```
