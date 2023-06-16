---
title: hexo 博客搭建教程
date: 2022-04-25 21:53:20
tags: hexo
category: 笔记
---

本文详细介绍了从开始搭建博客到自定义高级功能所经历的整个过程。

## 运行环境

- node
- git

## 搭建步骤

- 安装 hexo
- 通过 github page 免费建站
  - 创建 repository 
  - Settings 配置 page 站点
  - 个人 settings 配置 ssh


<!-- more -->

## 基础功能

-  read more ，首页仅显示文章摘要
  - 使用官方推荐 `<!-- more-->`标签截断 .md 文档

- 使用 typort + upic 编辑文档、建立图床
  - 也可使用 typora + picgo 实现图床


## 高级功能

- 自定义 landscape 主题
- valine + leancloud 实现无后端评论系统
- 使用阿里云域名实现域名转发
- rss 订阅
- 实现打赏功能
- 实现国内分享

## 踩坑

- 需要设置 github repository default 分支为 gh-pages
  - master 分支用于管理 hexo project 
  - git-pages 用于实现网站托管
- 通过 ssh 访问 github , username + password 登录方式无法使用
  - 也可通过 acesstoken 方式实现访问
- 通过 CNAME 实现域名转发，无须备案
  - 阿里云 url 转发需要备案
- 域名转发导致 css 样式失效
  - theme 主题，url 设置错误
- CNAME 如何避免被自动删除
  - 放在 source 文件夹下，避免被自动删除。
