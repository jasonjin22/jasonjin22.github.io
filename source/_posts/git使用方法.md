---
title: git使用方法
date: 2019-03-19 21:19:02
category: 学习
---
都已经是大三的人了，但是对git的用法还不是很熟悉，于是看了看廖雪峰的小站。虽然看完了之后还是没记住。

### 版本控制：分布式 VS 集中式

- 分布式安全
- 分布式不必联网
- 分布式有分支管理

### 创建版本库

- git init
- .git目录：跟踪管理版本库的
- git add
- git commit

### 时光机穿梭

- git status：查看仓库当前状态
- git diff：查看修改内容

### 版本回退

- git commit相当于保存一个快照，游戏存盘
- git log：查看commit的历史记录
- git用HEAD表示当前版本，上个版本HEAD^，上上个是HEAD^^，前100个是HEAD~100
- ```git reset --hard HEAD^```
- git reflog：查看命令历史以便确定要回到未来的哪个版本

### 工作区与暂存区

- 工作区（working directory）
  - 即init的文件夹
- 版本库：.git文件夹（repository）
  - 版本库中有一个暂存区（stage）
  - git add：工作区->stage， git commit：stage->分支

### 关于修改

- 每次修改，如果不add到stage里就不会被加入到commit
- `git checkout -- readme.txt`可以丢弃工作区的修改，有两种情况
  - 一种是`readme.txt`自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库(原始的repository)一模一样的状态
  - 一种是`readme.txt`已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态
  - `git checkout -- file`命令中的`--`很重要，没有`--`，就变成了“切换到另一个分支”的命令
- 用命令`git reset HEAD <file>`可以把暂存区的修改撤销掉（unstage），重新放回工作区
- 总结：
  - 场景1：当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令`git checkout -- file`。
  - 场景2：当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令`git reset HEAD <file>`，就回到了场景1，第二步按场景1操作。
  - 场景3：已经提交了不合适的修改到版本库时，想要撤销本次提交，进行版本回退，不过前提是没有推送到远程库。

### 删除文件

- 假设file已经存在于repository里了
  1. rm file（在工作区删除file）
  2. git rm file
  3. git commit -m "blabla"
- 如果将工作区的文件误删了，git checkout -- file
  - `git checkout`其实是用版本库里的版本替换工作区的版本，无论工作区是修改还是删除，都可以“一键还原”。



