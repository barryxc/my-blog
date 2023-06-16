---
title: sqlite3常用命令
date: 2023-06-15 16:04:12
tags:
category: sqlite3
---

### 官方下载地址

https://www.sqlite.org/download.html

<!-- more --> 

### 常用命令

| 命令                           | 描述                   |
| :----------------------------- | ---------------------- |
| `sqlite3  test.db`             | 创建或者打开数据库     |
| `.show`                        | 显示各种设置的当前值   |
| `.mode column`                 | 设置为表格模式         |
| `.headers on`                  | 展示表格头             |
| `.timer on`                    | 开启 cpu 定时器        |
| `.databases`                      | 查看有哪些数据库          |
| `.tables`                      | 查看有哪些表           |
| `.schema $table`          | 查看表概要             |
| `.indices ?table`                      | 查看索引，可选指定`table`         |
| `.backup $db $file`;            | 备份数据库到文件       |
| `.dump ?table`; | 以 `sql` 文本格式转储数据库，可选指定`table` |
| `.quit`;                       | 退出编辑模式  |
| `.help`;                       | 显示帮助信息  |
| `ctrl⌃+d`                     | 强制退出`sqlite3`程序 |

<!-- more -->

### 格式化输出

点命令后不能跟分号`;`

您可以使用下列的点命令来格式化输出为本教程下面所列出的格式：

```
sqlite>.header on
sqlite>.mode column
sqlite>.timer on
sqlite>
```


### `sqlite_master`

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
### `sqlite_sequence`

当`sqlite`数据库中包含自增列时，会自动建立一个名为 sqlite_sequence 的表。这个表包含两个列：`name`和`seq`。`name`记录自增列所在的表，`seq`记录当前序号（下一条记录的编号就是当前序号加1）。

```
sqlite> select * from sqlite_sequence;
```

### `autoincrement`

`sqlite` 的 **autoincrement** 是一个关键字，用于表中的字段值自动递增。我们可以在创建表时在特定的列名称上使用 **autoincrement** 关键字实现该字段值的自动增加。

关键字 `autoincrement` 的使用，必须满足以下两点:
**1、只能用于整型（INTEGER）字段，INT类型也不可以；**
**2、只能用于PRIMARY KEY字段；**


```
sqlite> create table if not exists $tablename ( _id integer primary key autoincrement , name text , age int );
```


### 获取表信息

```
sqlite> pragma table_info( $tablename ); 
```

### 创建表语句

```
sqlite> 
create table if not exists $table_name(
   $column1 datatype  primary key(one or more columns),
   $column2 datatype,
   $column3 datatype,
   .....
   $columnN datatype,
);
```

### 删除表 `truncate`

在 `sqlite` 中，并没有 `truncate table` 命令，但可以使用 `sqlite` 的 `delete` 命令从已有的表中删除全部的数据。

`delete` 命令的基本语法如下：

```
sqlite> delete from table_name;
```

但这种方法无法将递增数归零。

如果要将递增数归零，可以使用以下方法：

```
sqlite> delete from sqlite_sequence where name = $table_name;
```

### 更新数据

```
sqlite> insert or replace into $tablename ( ?,?,?,? ) values ( ?,?,?,? );
```

### 查询数据

```
sqlite> select * from $tablename where $col1=?;
```

### 删除数据

```
sqlite> delete from $tablename where $col1=?;
```

### [事务控制](https://www.runoob.com/sqlite/sqlite-transaction.html)

使用下面的命令来控制事务：

- `begin transaction`：开始事务处理。
- `commit`：保存更改，或者可以使用 `end transaction` 命令。
- `rollback`：回滚所做的更改。

### [索引](https://www.runoob.com/sqlite/sqlite-index.html)

使用 `create index` 语句创建索引，它允许命名索引，指定表及要索引的一列或多列，并指示索引是升序排列还是降序排列。索引也可以是唯一的，与 `unique` 约束类似，在列上或列组合上防止重复条目。

#### 创建单列索引

```
sqlite> create index $index_name on $table_name ( $column_name);
```

#### 创建联合索引

```
sqlite> create index $index_name on $table_name ( $column_name1 , $column_name2);
```

#### 创建联合唯一索引

```
sqlite> create unique index $index_name on $table_name ( $column_name1 , $column_name2);
```

#### 删除索引

```
sqlite> drop index $index_name;
```



### [约束](https://www.runoob.com/sqlite/sqlite-constraints.html)

约束是在表的数据列上强制执行的规则。这些是用来限制可以插入到表中的数据类型。这确保了数据库中数据的准确性和可靠性。约束可以是列级或表级。列级约束仅适用于列，表级约束被应用到整个表。以下是在 SQLite 中常用的约束。

- `not null` 约束：确保某列不能有 `null` 值。
- `default` 约束：当某列没有指定值时，为该列提供默认值。
- `unique` 约束：确保某列中的所有值是不同的。
- `primary key` 约束：唯一标识数据库表中的各行/记录。
- `check` 约束：`check` 约束确保某列中的所有值满足一定条件。



### [触发器](https://www.runoob.com/sqlite/sqlite-trigger.html)

`sqlite` 触发器（`trigger`）是数据库的回调函数，它会在指定的数据库事件发生时自动执行/调用。

创建触发器

- `sqlite` 的触发器（`trigger`）可以指定在特定的数据库表发生 `delete`、`insert` 或 `update` 时触发，或在一个或多个指定表的列发生更新时触发。

- `before` 或 `after` 关键字决定何时执行触发器动作，决定是在关联行的插入、修改或删除之前或者之后执行触发器动作。

```
create  trigger $trigger_name [BEFORE|AFTER] $event_name of $column_name on $table_name
begin
 -- 触发器逻辑....
end;
```

查看触发器

```
sqlite> select name from sqlite_master
where type = 'trigger';
```

删除触发器

```
sqlite> drop trigger $trigger_name;
```



### [`pragma`](https://www.runoob.com/sqlite/sqlite-pragma.html) 

`sqlite` 的 `pragma` 命令是一个特殊的命令，可以用在 `sqlite` 环境内控制各种环境变量和状态标志。一个 `pragma` 值可以被读取，也可以根据需求进行设置。

要查询当前的 `pragma` 值，只需要提供该 `pragma` 的名字：

```
pragma $pragma_name;
```

要为 `pragma` 设置一个新的值，语法如下：

```
pragma $pragma_name = $value;
```

