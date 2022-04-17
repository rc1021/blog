---
title: "SSH Copy"
date: 2022-04-17T14:43:52+08:00
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

如果你需要將檔案或目錄從本地上傳到遠程伺服器，或從遠程下載資料到本地電腦，可以使用 `scp` 達成。

## `scp` 指令用法

從本地位置複製到遠程位置 (上傳)

```
$ scp -r /path/from/local username@hostname:/path/to/remote
```

從遠程位置複製到本地位置 (下載)

```
$ scp -r username@hostname:/path/from/remote /path/to/local
```

加上自訂端口(Port)

```
$ scp -r -P xxxx username@hostname:/path/from/remote /path/to/local
```

說明:

1. `-r` 使用遞歸複製所有目錄和文件
1. `hostname` 將是主機名或 IP 地址
1. 如果需要自定義端口（除了端口 22），請使用 `-P portnumber`

恭喜你又學會一個技巧了

---

## 聽說：小故事大道理

來源 萬維鋼精英日課2：努力就有收獲不等於努力就能成功

「努力就有收穫」肯定是沒錯的，但我們得區別「努力就有收穫」和「努力就能成功」。現在我們關注的所謂「成功」，是指出類拔萃，是相對於大多數人，你是一個什麼位置。如果會努力的人很多，而具有開放頭腦和創造性思維的人很少，那麼「努力」就不是一個預測「成功」的好指標。

越是競爭激烈的領域，天賦和機遇就越重要。比如職業足球、音樂家這些領域，願意勤學苦練的人實在太多了，最後勝出的肯定得有點天賦。如果一個領域僅僅是努力就能比別人領先很多，那只能說明願意進入這個領域的高手太少。
