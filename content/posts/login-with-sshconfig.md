---
title: "透過 SSH config 登入遠端伺服器"
date: 2022-04-16T21:38:14+08:00
tags: ['ssh']
draft: false
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
draft: false
---

如果你經常通過 SSH 連接到多個遠程系統，你會發現記住所有遠程 IP 地址、不同的用戶名、非標準端口和各種命令行選項是很困難的，如果可以的話，通常會配置 `SSH config` 記住這些資訊。

## 先決條件

假設在你的系統裡 `~/.ssh` 目錄已經存在且安裝了 OpenSSH。

## 新增 SSH 配置文件

默認情況下，SSH 配置文件可能不存在，因此請使用 `touch` 命令建立它(windows 用戶直接新增檔案)

```
$ touch ~/.ssh/config
```

設定權限不讓其它用戶有權更新

```
$ chmod 600 ~/.ssh/config
```

## SSH 配置文件結構

文件結構一共 2 層：

```
Host {IDENTIFY NAME}
    {SSH_OPTION} {VALUE}
    {SSH_OPTION} {VALUE}
Host {IDENTIFY NAME}
    {SSH_OPTION} {VALUE}
    {SSH_OPTION} {VALUE}
```

- 第 1 層為 節點名稱(連線別名)
- 第 2 層為 SSH Option (像是 User, IP, IdentityFile) + 值

## 命令改為配置內容

通過 SSH 連接到遠程服務器時，你會使用遠程用戶名稱、主機 IP 位置和端口，下面例子說明使用 SSH 命令以名為 `ubuntu` 的用戶身份登入 `example.com:2222` 主機

```
// EXAMPLE 1
$ ssh ubuntu@example.com -p 2222
```

編輯 `~/.ssh/config` 將上述命令用配置的方式呈現會得到這樣的內容：

```
Host example_1
    HostName example.com
    User ubuntu
    Port 2222
```

現在，你可以用下面命令登入遠程主機了

```
$ ssh example_1
```

恭喜你又學會一個技巧了

---

## 聽說：小故事大道理

來源 羅振宇2022跨年演講

有一個家庭，家裡有一個老太太和兩個孩子。前幾十年一家人節衣縮食，供老大讀書。後來老大有了出息，開了工廠、賺了錢。老二呢，生活還比較困難。那麼這個老太太會怎麼處理兩個孩子的關係呢？

她可能會這麼做：第一，想方設法讓老大拉扯老二一把，可能是金錢上的，也可能是機會上的。第二，她也會敦促老二向老大學習，要領老大的情。第三，她希望老大拉扯老二的這個情分，不是固定按月給錢，而是更走心的安排，比如經常送盤餃子，或者帶著老二去見見世面，等等。

這其實是 `共同富裕` 這個觀點的表現：一部分人先富起來，然後自願幫助暫時落後的人。這樣樸素的道德直覺往往才能到達事物的本質，這樣才是幸福該有的樣子。
