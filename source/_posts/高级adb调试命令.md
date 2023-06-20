---
title: 高级adb调试命令
date: 2022-04-24 12:36:49
tags:
  - adb
  - android
category: android
---

## 用某个用户的权限来执行

```shell
run-as $package_name
```

例如：查看sp文件

```shell
adb shell
run-as $package_name
cd shared_prefs
cat $file_name
```

<!-- more -->

## 截屏

```shell
adb shell screencap /sdcard/$file_name
adb shell pull /sdcard/$file_name ~/desktop/$file_name
```

## 录屏

```shell
adb shell record /sdcard/$video_file_name
```

## wifi 调试

```shell
adb tcpip 5555
adb connect $ip_address:5555
```

## 查看指定包名的进程 id

```shell
adb shell ps | grep '$package_name'
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
keytool -list -v -keystore $keystore_file
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
 adb pull xxx.apk ~/desktop/$apk_file_name  #转储apk
```

## 清除应用数据

```shell
adb shell pm clear $package_name
```

## 覆盖安装 apk

```shell
adb install xxx.pk
adb install -r xxx.apk  覆盖安装
```

## 卸载 apk

```shell
adb uninstall $package_name
adb uninsatll -k $package_name  
# 保留数据卸载 
adb shell pm uninstall -k  $package_name 
```

## AAPT 查看 apk 信息

```shell
#列出压缩文件(zip,jar,apk)中的目录内容
 aapt l[ist] [-v] [-a] xxx.{zip,jar,apk}
 #转储apk文件信息
 aapt dump badging $file_name.apk
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

```shell
adb backup -f xxx.ab -noapk xxxx包名
adb restore xxx.ab

备份文件解析工具：safemobile 手机芯片取证系统
```

## 抓取系统崩溃和ANR日志

```shell
输出系统崩溃日志
系统应用：
adb shell dumpsys dropbox system_app_crash --print > crash.txt
adb shell dumpsys dropbox system_app_anr --print > anr.txt
三方应用：
adb shell dumpsys dropbox data_app_crash --print > crash.txt
adb shell dumpsys dropbox data_app_anr --print > anr.txt
```

## 查看内存信息

```shell
#[查看系统进程内存信息分布情况]
adb shell dumpsys meminfo $package_name
#[查看当前应用内存情况]
adb shell dumpsys meminfo $package_name
#[查看安装包信息]
adb shell dumpsys package $package_name
#[查看当前应用安装包信息]
adb shell dumpsys package $package_name
```
