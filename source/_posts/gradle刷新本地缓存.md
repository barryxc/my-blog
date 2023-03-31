---
title: gradle刷新本地缓存
date: 2023-03-31 14:38:32
tags:
category:
---

方式1 ：If you are using a recent version of Gradle, you can use --refresh-dependencies option.

```java
./gradlew build --refresh-dependencies
```



方式2：On Unix systems, you can delete all the existing artifacts (artifacts and metadata) Gradle has downloaded using:

```java
rm -rf $HOME/.gradle/caches/
```
