---
title: "Git常用指令集"
date: 2022-04-28T09:18:36+08:00
tags: []
draft: true
showToc: true
TocOpen: true
hidemeta: false
comments: false
# description: "短描述"
# hideSummary: false
searchHidden: false
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: true
---

這裡筆記一些 git command line 的用法

## 將本地分支重置遠程某個提交

如果你有機會同時在兩台電腦工作，本地分支可能要重置為遠程分支的某個提交

```
$ git reset --hard <commit-hash>
```
