---
title: mac装机必备
date: 2024-01-18 11:54:21
tags: mac装机必备
category: mac装机必备
---

#### 软件工具

1. 安装 `hombrew` 包管理器 https://brew.sh/

2. 安装 `iterm2` 工具 https://iterm2.com/

3. 安装 `oh-my-zsh` 插件 https://ohmyz.sh/

4. 安装 `git` 命令行工具 `brew install git` https://git-scm.com/

   <!--more-->

5. 安装 `git-cz` 插件 https://github.com/commitizen/cz-cli

   ```shell
   npm install -g commitizen
   npm install -g cz-conventional-changelog
   echo '{ "path": "cz-conventional-changelog" }' > ~/.czrc
   ```

6. 安装 `jdgui` 工具 https://java-decompiler.github.io/

7. 安装 `jadx` 工具 https://github.com/skylot/jadx

8. 安装 `apktool` 反编译以及重打包 工具 https://apktool.org/

9. 安装 `ghidra` 反编译工具(c/c++反编译) https://github.com/NationalSecurityAgency/ghidra

10. 安装 `colc` 代码统计工具 https://github.com/AlDanial/cloc?tab=readme-ov-file#install-via-package-manager

11. 安装 `node` 环境 `--global` 全局安装 https://nodejs.org/en

12. 安装 `typora` 以及  `PicList` 图床软件, 设置 `github` 图床 https://piclist.cn/

13. 安装 `hexo` 工具 https://hexo.io/zh-cn/

14. 安装 `postman` 网络请求工具 https://www.postman.com/

15. 安装 `alfred` 工具 https://www.alfredapp.com/

16. 安装`youdao`有道翻译工作流插件 https://github.com/wensonsmith/YoudaoTranslator

17. 安装 `sublime` https://www.sublimetext.com/ 

18. 安装 `submlime HTML-CSS-JS Prettify` 插件，步骤： `Tools`->`Command Palette`->`Package Control:Install Package ` 

19. 安装 `submlime shellcheck `插件，步骤： `Tools`->`Command Palette`->`Package Control:Install Package ` 

20. 安装 `vscode` 开发工具 https://code.visualstudio.com/

21. 安装 `idea` 开发工具 https://www.jetbrains.com/zh-cn/idea/

22. 安装 `Clion` 开发工具 https://www.jetbrains.com.cn/clion/

23. 安装 `charles` 抓包工具 https://www.charlesproxy.com/

24. 安装 `android studio`开发工具 https://developer.android.com/studio

### 环境配置

1. 配置 `ssh` 环境、`github ssh` 环境
2. 配置 `.zshrc` 配置文件以及`PATH`环境变量

  ```
  export ANDROID_HOME=/Users/$USER/Library/Android/sdk
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

3. 添加当前目录到 PATH 中，可以避免每次执行文件时添加 `./ `前缀:  `export PATH=${PATH}:.`

4. 解决 `git` 中文路径显示 `unicode` 代码问题 `git config --global core.quotepath false`

5. 操作：在当前的目录中打开 `iterm2  `命令行工具 : https://support.apple.com/zh-cn/guide/terminal/trmlb20c7888/mac
