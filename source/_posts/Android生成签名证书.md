---
title: Android生成签名证书
date: 2023-08-30 11:33:16
tags:
category:
---

## 生成秘钥证书

```shell
 keytool -genkey -alias "xxxx" -keystore "healkit.keystore" -keyalg rsa -keysize 2048
```

## 查看证书信息

```shell
keytool -list -keystore healkit.keystore -v
```
