---
title: gradle参数传递踩坑
date: 2023-12-12 00:28:58
tags:
category:
---


gradle 参数传递默认为 `string` 类型
```shell
./gradlew -Pflag=false
```
参数为字符串类型时，这里判断为始终为真
```groovy
//错误
if (flag) {
  //todo
}


//正确
if (Boolean.valueOf(flag)) {
   //todo
}
```
