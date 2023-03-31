---
title: adb常见链接问题
date: 2023-03-31 14:39:27
tags:
category:
---

1. 没有开启手机开发者模式以及USB调试模式
2. USB 连接方式设置为仅充电
3. 数据线不能传输数据
4. 电脑 usb 驱动有问题，重启电脑
5. 手机系统问题，重启手机



WIFI 调试 offline 问题：

1. 重启开发者选项
2. 重启 adb server  

```java
adb kill-server
adb start-server
```
