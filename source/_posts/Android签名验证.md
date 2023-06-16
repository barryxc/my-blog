---
title: Android签名验证
date: 2023-03-31 14:31:47
tags: 签名
category: android
---

```shell
apksigner verify  -v  文件路径
```

### 人工简单查看



1. 解压 apk/META-INF/，找到 .SF文件，（一般是 CERT.SF 文件 ），如果不存在说明不存在 v1 签名。



1. 解压apk/META-INF/XXXX.SF(如CERT.SF，不是MANIFEST.SF)，查看开始部分，如果不包含X-Android-APK-Signed字样则为v1， 如：



```shell
Signature-Version: 1.0
SHA1-Digest-Manifest-Main-Attributes: NdvTTYSDLv+xfCdISs2OUVv3OXY=
Created-By: 1.6.0_37 (Sun Microsystems Inc.)
SHA1-Digest-Manifest: sN1jczINBspGueVoYodPfvNRYKA=
```



1. 包含X-Android-APK-Signed字样，则冒号后面跟的版本就是签名版本，如下面是v1和v2版本



```latex
Signature-Version: 1.0
Created-By: 1.0 (Android)
SHA1-Digest-Manifest: EsSraWdS5nUZen7L+SDZDNTr230=
X-Android-APK-Signed: 2
```



1. 包含X-Android-APK-Signed字样，则冒号后面跟的版本就是签名版本，如下面是v2和v3版本



```latex
Signature-Version: 1.0
Created-By: 1.0 (Android)
SHA1-Digest-Manifest: EsSraWdS5nUZen7L+SDZDNTr230=
X-Android-APK-Signed: 2, 3
```



<!-- more -->

### 工具查看(通过工具会输出详细的签名信息)



在SDK/build-tools/版本（如30.0.2）/apksigner.bat或SDK/build-tools/版本（如30.0.2）/lib/apksigner.jar两种工具。



- 工具一使用：



```latex
SDK/build-tools/版本（如30.0.2）/apksigner.bat verify --verbose xxx.apk
```



- 工具二使用：



```latex
java -jar SDK/build-tools/版本（如30.0.2）/lib/apksigner.jar --verbose xxx.apk
```



示例(v1+v2)：



```latex
E:\Android\Sdk\build-tools\30.0.2\apksigner.bat verify --verbose .\cdd.apk
&nbsp;
Verifies
Verified using v1 scheme (JAR signing): true
Verified using v2 scheme (APK Signature Scheme v2): true
Verified using v3 scheme (APK Signature Scheme v3): false
Verified using v4 scheme (APK Signature Scheme v4): false
Verified for SourceStamp: false
Number of signers: 1
```



示例（v1）：



```latex
Verifies
Verified using v1 scheme (JAR signing): true
Verified using v2 scheme (APK Signature Scheme v2): false
Verified using v3 scheme (APK Signature Scheme v3): false
Verified using v4 scheme (APK Signature Scheme v4): false
Verified for SourceStamp: false
Nuer of signers: 1
```



## 更详细说明



https://developer.android.com/studio/command-line/apksigner?hl=zh-cn#options
