---
title: git 笔记
date: 2022-04-26 09:58:19
tags: git
category: git
---

## [Git 官网](https://git-scm.com/)

命令文档地址：https://git-scm.com/docs

## 检查本地 git 环境

```
git --version
```

## [主要命令](https://git-scm.com/)

##  Branch 

```
git branch
```

<!-- more -->

在 Git 命令中，`branch` 和 `refspec` 是两个不同的概念，它们的语法也不同。

### Branch 语法

`branch` 是指本地或远程的分支名。在 Git 命令中，您通常只需要提供分支名即可，例如：

```
1# 切换到一个已存在的本地分支
2git checkout branch-name
3
4# 创建并切换到一个新的本地分支
5git checkout -b new-branch-name
6
7# 删除一个本地分支
8git branch -d branch-name
9
10# 拉取远程分支并在本地创建一个跟踪分支
11git checkout --track origin/remote-branch-name
```

在这些命令中，`branch-name` 和 `new-branch-name` 是本地分支名，而 `origin/remote-branch-name` 是远程分支名，其中 `origin` 是远程仓库的默认名称。

### Refspec 语法

`refspec` 在 `git fetch` 和 `git push` 命令中定义了源分支和目标分支之间的映射关系，在其最基本的形式中，`refspec` 的语法是：

```
source:destination
```

它可能具有以下形式：

- `+source:destination` - 强制推送（忽略非快进更新）
- `source` - 指定只推送源分支到远程同名分支
- `:destination` - 删除远程的目标分支（使用 `git push`）

在 `git push` 的上下文中，`source` 通常是本地分支名，而 `destination` 是远端分支名。而在 `git fetch` 的上下文中，则是相反：`source` 是远端分支名，而 `destination` 是本地分支名。

例如，如果您想要推送本地的 `feature` 分支到远程仓库的 `feature` 分支，您会使用：

```
git push origin feature:feature
```

如果您想要强制推送这个分支（即使这会导致数据丢失），则会使用：

```
git push origin +feature:feature
```

如果您想要删除远程仓库的 `feature` 分支，则会使用：

```
git push origin :feature
```

而如果您想要从远程仓库获取 `feature` 分支并将其映射到本地的 `my-feature` 分支上，您会使用：

```
git fetch origin feature:my-feature
```

在这里，`origin` 是远程仓库的名称。对于 `git fetch` 和 `git push`，您也可以省略 `destination` 部分，让 Git 使用默认的行为（如将分支推送到具有相同名称的远程分支）。

### 总结

- `branch` 通常只是分支的名称，无需特殊语法。
- `refspec` 是一个更复杂的概念，用于在 `git fetch` 和 `git push` 操作中定义本地分支和远程分支之间的映射关系，有自己特定的语法。
