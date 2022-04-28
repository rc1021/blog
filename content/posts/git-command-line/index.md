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

## 新增指令別名

有時指定參數很長，你可以用 alias 設定指令別名

```
$ git config --global alias.log-graph 'log --graph --all --decorate --oneline'

$ git log-graph
* 4b35929 (HEAD -> main, origin/main, origin/HEAD) 新增文章：Git常用指令集
* 6f207d9 update
* 3186a5b 新增Gather頁面
*   136775a Merge branch 'main' of github.com:rc1021/blog into main
|\
| * aef5629 更新文章內容
* | 90d614d 新增文章：免密碼登入遠程主機(SSH copy id)
|/
*   0565d3d Merge branch 'main' of github.com:rc1021/blog into main
```