---
title: "免密碼登入遠程主機(SSH copy id)"
date: 2022-04-22T11:15:59+08:00
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
---

如果你有 SSH 金鑰就能免密碼登入遠程主機

## 先決條件

- 假設在你的系統安裝了 OpenSSH。

## 產生 SSH 金鑰(假設你沒有)

執行 ssh-keygen 產生 ssh key

```
$ ssh-keygen 
Generating public/private rsa key pair.
Enter file in which to save the key ...
```

## 執行指令

假設你要登入的遠程指定為 `ssh {username}@{remote.ip}`

使用 `ssh-copy-id` 複製金鑰到遠程主機，這期間會問你登入密碼

```
$ ssh-copy-id {username}@{remote.ip}
The authenticity of host '{remote.ip}' can't be established.
ECDSA key fingerprint is xxxxxx.
Are you sure you want to continue connecting (yes/no)? yes
/usr/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed
/usr/bin/ssh-copy-id: INFO: 1 key(s) remain to be installed -- if you are prompted now it is to install the new keys
{username}@{remote.ip}'s password: 
```

說明:

- `username` 是你遠程主機的用戶名稱
- `remote.ip` 是遠程 IP 地址

## 免密碼登入

現在你登入不需要密碼了

```
$ ssh {username}@{remote.ip}
```

恭喜你又學會一個技巧了

---

## 聽說：小故事大道理

來源 羅胖60秒：什麼叫退休?

話說矽谷投資人納瓦爾，對「退休」這個詞有一個很有趣的定義。

什麼是退休？不是不工作，而是不再為了想象中的明天而犧牲今天，這就叫退休。按照這個定義，一個人的退休方式有很多種。

第一種方式當然是存夠了錢，想幹什麼就幹什麼，不為明天焦慮，這個人的狀態是退休。

第二種方法，是把開銷降到幾乎是零，比如說出家修行，那也不用為了明天焦慮，他也退休了。

其實還有第三種方法，就是做自己熱愛的事，能不能掙得到錢無所謂，這種方法最好。為什麼？因為通常做自己熱愛的事，就是找到了最獨特的價值。

