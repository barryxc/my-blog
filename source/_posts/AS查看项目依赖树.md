---
title: AS查看项目依赖树
date: 2023-03-31 14:33:24
tags: as
category: android
---

#### 方式一

```java
./gradlew :模块名:dependencies  --scan 
./gradlew :模块名:dependencies  > xx.log 
```

#### 方式二

输入：

```java
./gradlew build --scan
```

出现

![img](https://intranetproxy.alipay.com/skylark/lark/0/2023/png/3756563/1675751747423-7a38c8aa-f7b5-4617-a72a-4b397a8b7f43.png)

输入yes

生成网址：

![img](https://intranetproxy.alipay.com/skylark/lark/0/2023/png/3756563/1675751788849-e8c61be8-fe70-43f4-b3b1-69e6ef5b4668.png)

点击网站查看

#### 方式三

使用 Gradle Project

![img](https://intranetproxy.alipay.com/skylark/lark/0/2023/png/3756563/1675752215256-2819385e-1548-4705-8b5e-8757b7d6966a.png)
