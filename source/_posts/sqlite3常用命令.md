---
title: sqlite3常用命令
date: 2023-06-15 16:04:12
tags:
category: sqlite3
---



## 官方下载地址

https://www.sqlite.org/download.html

## 常用命令

| 命令                           | 描述                   |
| :----------------------------- | ---------------------- |
| `sqlite3  test.db`             | 创建或者打开数据库     |
| `.show`                        | 显示各种设置的当前值   |
| `.mode column`                 | 设置为表格模式         |
| `.header on`                   | 展示表格头             |
| `.timer on`                    | 开启 cpu 定时器        |
| `.tables`                      | 查看有哪些表           |
| `.schema`                      | 查看表概要             |
| `backup $db $file`;            | 备份数据库到文件       |
| `ctrl⌃+d`                     | 强制退出 sql 编辑模式  |
| `.quit`;                       | 退出sqlite3 shell程序  |
| `.help`;                       | 显示帮助信息  |



## 格式化输出

您可以使用下列的点命令来格式化输出为本教程下面所列出的格式：

```
sqlite>.header on
sqlite>.mode column
sqlite>.timer on
sqlite>
```



## sqlite_master

主表中保存数据库表的关键信息，并把它命名为 **sqlite_master**。如要查看表概要，可按如下操作：

```
sqlite>.schema sqlite_master
```

这将产生如下结果：

```
CREATE TABLE sqlite_master (
  type text,
  name text,
  tbl_name text,
  rootpage integer,
  sql text
);
```

