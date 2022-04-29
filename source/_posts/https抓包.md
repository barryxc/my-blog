---
title: android https 抓包
category: android
date: 2022-04-26 11:30:54
tags:
  - android
  - Charles
  - https
---

### 网络安全配置

android 系统高于 7.0 ,配置网络安全策略

```plain
android:networkSecurityConfig="@xml/network_security_config"
```

```plain
<?xml version="1.0" encoding="utf-8"?>
<network-security-config>
    <base-config cleartextTrafficPermitted="true">
        <trust-anchors>
            <certificates src="system" overridePins="true" />
            <certificates src="user" overridePins="true" />
        </trust-anchors>
    </base-config>
</network-security-config>
```

<!-- more -->

### 手机下载安装证书

```plain
Charles:

安卓手机类型众多，所以有些不太一样，

方法一：

1、打开Charles，选择help→SSL Proxying→Install Charles Root Certificate on a Mobile Device or Remote Browser

2、手机连接电脑代理，打开浏览器，输入网址：chls.pro/ssl

3、手机弹出提示：安装配置描述文件。您要允许吗？忽略|允许，选择允许，即可

方法二：

1、打开Charles，选择help→SSL Proxying→Save Charles Certificate，将证书导入到手机中

2、导入后直接点击安装证书即可

方法三：

1、打开Charles，选择help→SSL Proxying→Save Charles Certificate，将证书导入到手机中

2、导入后直接点击安装证书，提示无法打开

3、进入手机设置 → 更多设置 → 系统安全 → 从存储设备安装 → 选择charles.pem，点击高级，安装证书即可

常见手机：小米手机，vivo,华为手机，需要设置手机锁屏密码
```

```
有的手机 .pem 格式的证书没法直接点击安装，需要修改后缀为.crt 格式，才能点击安装
```

### 开启代理

![img](https://intranetproxy.alipay.com/skylark/lark/0/2021/png/3756563/1618564185975-da945211-f8fe-4f36-82e3-c4fe9e63239d.png)

##

## 踩坑：chls 证书和电脑是绑定的关系

连接每台新电脑都需要安装新的 chls 证书
