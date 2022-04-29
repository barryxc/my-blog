---
title: 常用adb命令
date: 2022-04-24 12:36:49
tags: adb android
category: adb
---

## 查看缓存文件

```
adb shell
run-as xxx包名
cd shared_prefs
cat xxx文件名
```

## 抓取日志

```shell
adb shell logcat --pid=xxx "tag:priority"  > ~/desktop/xx
.log
```

<!-- more -->

## 截屏

```shell
adb shell screencap /sdcard/xx.png
adb shell pull /sdcard/xx.png ~/desktop/xx.png
```

## 录屏

```shell
adb shell record /sdcard/xx.mp4
```

## wifi 调试

```shell
adb tcpip 5555
adb connect 192.168.xx.xx:5555
```

## 查看指定包名的进程 id

```shell
adb shell ps | grep "包名"
```

## 获取 apk 签名

```shell
#1. 将apk解压；
#2. 找到META-INF 下的.RSA文件；
#3. 进入shelll环境，进入.RSA文件文件所在路径，执行命令：
keytool -printcert -file XXX.RSA即可查看签名信息。
```

## 获取 keystore 签名

```shell
#keystore在jdk安装目录bin文件夹下面
keytool -list -v -keystore xxx(keystore文件)
```

## 获取手机分辨率

```shell
adb shell wm size
```

## 查看屏幕密度

```shell
adb shell wm density
```

## 获取所有已安装 apk

```shell
adb shell pm list package
```

## 获取已安装 apk 文件路径

```shell
 adb shell pm path 包名
 adb pull xxx.apk ~/desktop/xx.apk  #转储apk
```

## 清除应用数据

```shell
adb shell pm clear 包名
```

## 覆盖安装 apk

```shell
adb install xxx.pk
adb install -r xxx.apk  覆盖安装
```

## 卸载 apk

```shell
adb uninstall 包名
adb uninsatll -k 包名  保留数据卸载(adb shell pm uninstall -k  xxx )
```

## AAPT 查看 apk 信息

```shell
#列出压缩文件(zip,jar,apk)中的目录内容
 aapt l[ist] [-v] [-a] xxx.{zip,jar,apk}
 #转储apk文件信息
 aapt dump badging xxx.apk
```

## 抓取数据库

```shell
adb shell mkdir /sdcard/databases
adb shell run-as 包名
cp databases /sdcard/databases
exit
adb pull /sdcard/databases  ~/desktop
```

## 已连接设备

```shell
adb devcies
```

## 重启手机

```shell
adb -s xxx（手机序列号） reboot
```

## 备份与还原

```
adb backup -f xxx.ab -noapk xxxx包名
adb restore xxx.ab

备份文件解析工具：safemobile 手机芯片取证系统
```
