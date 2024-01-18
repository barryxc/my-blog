---
title: mac 常用配置
date: 2024-01-18 11:54:21
tags:
category:
---

1. 在当前的目录中打开 `iterm2  `命令行工具

   ![image-20240118140115273](/Users/bytedance/Library/Application Support/typora-user-images/image-20240118140115273.png)

2. 添加当前目录到 PATH 中，可以避免每次执行文件时添加 `./`前缀

   ```shell
   export PATH=${PATH}:.
   ```

3. 安装 `iterm2` 工具，安装 `oh-my-zsh` 插件

   `iterm2:` https://iterm2.com/

   `oh-my-zsh:` https://ohmyz.sh/

4. 安装 `git-cz` 插件，[链接](https://github.com/commitizen/cz-cli)

   ```
   npm install -g commitizen
   npm install -g cz-conventional-changelog
   echo '{ "path": "cz-conventional-changelog" }' > ~/.czrc
   ```

   - [x] https://github.com/commitizen/cz-cli

5. 安装 `node` 环境 

   - [x] https://nodejs.org/en
