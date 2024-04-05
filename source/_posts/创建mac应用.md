---
title: 创建mac应用
date: 2024-04-05 14:48:41
tags:
category: mac app
---

# 如何为一个 sh 脚本创建 mac 应用程序？

**创建捆绑包目录结构**： 在 Finder 中，创建一个新的文件夹来作为应用程序捆绑包的根目录，并以 `.app` 扩展名命名，例如 `MyShellApp.app`。

**创建 Contents 目录**： 在 `MyShellApp.app` 目录内部，创建一个名为 `Contents` 的子目录。

**创建 MacOS 目录**： 在 `Contents` 目录内部，创建一个名为 `MacOS` 的子目录。这是可执行文件的存放位置。

**创建 Info.plist 文件**： 在 `Contents` 目录中创建一个名为 `Info.plist` 的属性列表文件。这个文件包含了应用程序的元数据。以下是一个基本的 `Info.plist` 示例：

<!--more-->

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
    <key>CFBundleExecutable</key>
    <string>MyShellScript</string>
    <key>CFBundleName</key>
    <string>MyShellApp</string>
    <key>CFBundleVersion</key>
    <string>1.0</string>
    <key>CFBundlePackageType</key>
    <string>APPL</string>
    <key>CFBundleIconFile</key>
    <string>MyAppIcon.icns</string>
</dict>
</plist>
```

请替换相关键的值以匹配你的应用程序信息。

**添加你的脚本到 MacOS 目录**： 将你的 shell 脚本复制到 `MacOS` 目录，并重命名为在 `Info.plist` 中指定的 `CFBundleExecutable` 的值，例如 `MyShellScript`。确保脚本具有可执行权限：

```sh
chmod +x MyShellApp.app/Contents/MacOS/MyShellScript
```

**添加应用程序图标**： 如果你有一个应用程序图标（`.icns` 文件），将其复制到 `Contents/Resources` 目录（如果不存在，则创建它），并在 `Info.plist` 文件中添加对应的键值对：

```xml
<key>CFBundleIconFile</key>
<string>MyAppIcon.icns</string>
```

**测试应用程序**： 移动 `MyShellApp.app` 文件夹到mac 应用程序目录，点击应用图标来运行你的应用。
