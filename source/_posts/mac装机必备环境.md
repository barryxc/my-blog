---
title: mac安装环境
date: 2024-01-18 11:54:21
tags: mac
category: mac
---

1. 安装 `hombrew` 包管理器 https://brew.sh/

2. 安装 `iterm2` 工具 https://iterm2.com/

3. 安装 `oh-my-zsh` 插件 https://ohmyz.sh/

4. 添加当前目录到 PATH 中，可以避免每次执行文件时添加 `./ `前缀:  `export PATH=${PATH}:.`

5. 安装 `git` 命令行工具 `brew install git`

   <!--more-->

6. 安装 `git-cz` 插件 https://github.com/commitizen/cz-cli

   ```shell
   npm install -g commitizen
   npm install -g cz-conventional-changelog
   echo '{ "path": "cz-conventional-changelog" }' > ~/.czrc
   ```

7. 安装 `jdgui` 工具 https://java-decompiler.github.io/

8. 安装 `jadx` 工具 https://github.com/skylot/jadx

9. 安装 `apktool` 反编译以及重打包 工具 https://apktool.org/

10. 安装 `ghidra` 反编译工具( nasa 研发的 c++ 反编译工具) https://github.com/NationalSecurityAgency/ghidra

11. 安装 `colc` 代码统计工具 https://github.com/AlDanial/cloc?tab=readme-ov-file#install-via-package-manager

12. 安装 `node` 环境 ,`--global` 全局安装 https://nodejs.org/en

13. 安装 `typora` 以及  `PicList` 图床软件, 设置 `github` 图床 https://piclist.cn/

14. 安装 `hexo` 工具 `https://hexo.io/zh-cn/`
15. 安装 `alfred` 工具 https://www.alfredapp.com/

16. 安装`yd`有道翻译工作流插件 https://github.com/wensonsmith/YoudaoTranslator

17. 安装 `sublime` , 安装 `HTML-CSS-JS Prettify` 插件、 安装 `shellcheck `插件，步骤： `Tools`->`Command Palette`->`Package Control:Install Package ` 

18. 安装常用 `ide` 集成开发环境

    | IDE              |
    | ---------------- |
    | `vscode`         |
    | `idea`           |
    | `Clion`          |
    | `sublime text`   |
    | `charles`        |
    | `android studio` |

19. 配置 `ssh` 环境、`github ssh` 环境

20. 配置 `.zshrc` 环境变量以及`PATH`

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

21. 解决 `git` 中文路径显示 `unicode` 代码问题 `git config --global core.quotepath false`

22. 操作：在当前的目录中打开 `iterm2  `命令行工具 : https://support.apple.com/zh-cn/guide/terminal/trmlb20c7888/mac
