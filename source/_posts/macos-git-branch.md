---
title: 解决在 Mac OS 下终端无法显示 git 当前分支的情况
date: 2018-11-12 00:02:35
tags: 
 - terminal
 - git
categories: MacOS
---

编辑 .bash_profile 文件

```bash
# 编辑 .bash_profile
vi .bash_profile

# 若不存在，则新建
touch .bash_profile
vi .bash_profile
```
将下列代码复制粘贴到 .bash_profile 的末尾，保存后重启终端即可。

```bash
# Git branch in prompt.
function git_branch {
   branch="`git branch 2>/dev/null | grep "^\*" | sed -e "s/^\*\ //"`"
   if [ "${branch}" != "" ];then
       if [ "${branch}" = "(no branch)" ];then
           branch="(`git rev-parse --short HEAD`...)"
       fi
       echo " ($branch)"
   fi
}
 
export PS1='\u@\h \[\033[01;36m\]\W\[\033[01;32m\]$(git_branch)\[\033[00m\] \$ '
```
显示效果
![分支显示](macos-git-branch/branch.jpg)