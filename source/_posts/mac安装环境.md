---
title: mac安装环境
date: 2024-01-18 11:54:21
tags: mac
category: mac
---

1. 安装 `hombrew` 包管理器

   * https://brew.sh/

2. 安装 `iterm2` 工具，安装 `oh-my-zsh` 插件

   - `iterm2:` https://iterm2.com/

   - `oh-my-zsh:` https://ohmyz.sh/

3. 添加当前目录到 PATH 中，可以避免每次执行文件时添加 `./ `前缀

   ```shell
   export PATH=${PATH}:.
   ```

4. 安装 `git` 命令行工具

   ```shell
   brew install git
   ```

5. 安装 `jadx` 工具

   1. [链接](https://github.com/skylot/jadx)

6. 安装 jdgui 工具

   1. [链接](https://java-decompiler.github.io/)

7. 安装 `git-cz` 插件，[链接](https://github.com/commitizen/cz-cli)

   ```shell
   npm install -g commitizen
   npm install -g cz-conventional-changelog
   echo '{ "path": "cz-conventional-changelog" }' > ~/.czrc
   ```

   * https://github.com/commitizen/cz-cli

   <!--more-->

8. 在当前的目录中打开 `iterm2  `命令行工具 : [链接](https://support.apple.com/zh-cn/guide/terminal/trmlb20c7888/mac)	
   - 从访达打开新的“终端”窗口或标签页

9. 安装 `node` 环境 ,`--global` 全局安装
   - https://nodejs.org/en

10. 通过 `typora` 图像设置安装  `PicList` 图床软件, 设置 `github` 图床

   - https://piclist.cn/

11. 解决 `git` 中文路径显示 `unicode` 代码问题

    ```shell
    git config --global core.quotepath false
    ```

12. 安装 `hexo` 工具
    - `Hexo`https://hexo.io/zh-cn/

13. 安装 `alfred` 工具，创建 `yd`有道翻译工作流
    - `Alfred`:https://www.alfredapp.com/
    - `yd` `workflow`:https://github.com/wensonsmith/YoudaoTranslator

14. 安装常用 `ide` 集成开发环境

    1. `android studio` 
    2. `vscode` 
    3. `idea`
    4. `Clion`
    5. `typora`
    6. `sublime text`
       1. 打开命令面板，安装 `HTML-CSS-JS Prettify` 插件。步骤： `Tools`->`Command Palette`->`Package Control:Install Package ` 
       2. 安装 `shell check` 插件,步骤同上
    7. `charles`
    8. `Sourcetree`

15. 配置 `ssh` 环境、`github ssh` 环境

16. 配置 `.zshrc` 环境变量以及`PATH`

    ```shell
    export ANDROID_HOME=/Users/$USER/Library/Android/sdk
    export ANDROID_AVD_HOME=/Users/$USER/.android/avd
    export JAVA_HOME=$(/usr/libexec/java_home)
    export ANDROID_NDK_HOME=${ANDROID_HOME}/ndk/21.1.6352462
    
    export PATH=${PATH}:${ANDROID_HOME}/platform-tools/
    export PATH=${PATH}:${ANDROID_HOME}/tools/
    export PATH=${PATH}:${ANDROID_HOME}/tools/bin/
    export PATH=${PATH}:${ANDROID_NDK_HOME}/
    export PATH=${PATH}:${ANDROID_NDK_HOME}/toolchains/arm-linux-androideabi-4.9/prebuilt/darwin-x86_64/bin/
    export PATH=${PATH}:${ANDROID_HOME}/build-tools/34.0.0/
    export PATH=${PATH}:.
    ```

    
