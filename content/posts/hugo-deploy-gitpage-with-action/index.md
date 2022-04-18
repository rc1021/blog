---
title: "使用Git Actions佈署Hugo到GitPage"
date: 2022-04-18T10:16:16+08:00
tags: ['hugo', 'gitpage', 'deploy with github']
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

如果你知道 GitPage 且試著將 JAMStack(Hugo, Jekyll) 的內容自動佈署到 GitPage，這篇內容是一個很棒的起點。

## 先決條件

- 假設你已擁有 `{username}.github.io` 的 repository，請先確保你擁有 [GitPage](https://pages.github.com/) 再繼續。
- 假設你已擁有 Hugo 的 repository，請先確保你有一個 Hugo 專案且上傳至 github。
- 假設在你的系統裡 `~/.ssh` 目錄已經存在且安裝了 OpenSSH。

## 定義

首先我把 `repository` 稱為 `庫`

再來分清楚`來源庫`和`目標庫`是必要的：

- 目標庫：呈現站台的內容，這裡是指 `{username}.github.io` 專案
- 來源庫：這裡是指管理 Hugo 的專案，使用 `hugo new site blog` [參考手冊](https://gohugo.io/getting-started/quick-start/)

以我的站台來說 

- 目標庫是 [`rc1021/rc1021.github.io`](https://github.com/rc1021/rc1021.github.io)
- 來源庫是 [`rc1021/blog`](https://github.com/rc1021/blog)

你應該也擁有這樣兩個庫

## 產生佈署用的金鑰

我們的目標是自動化佈署，所以在庫與庫之間要聯系溝通你需要產生一組佈署用的金鑰，為了不影響本機的金鑰請使用下列命令

```
$ ssh-keygen -t rsa -b 4096 -C "{username}@users.noreply.github.com" -f ~/.ssh/noreply
```

- 請將 {username} 改為你的帳戶名稱

你將會得到 `noreply.pub` 和 `noreply` 兩個檔案

## 安裝公鑰至目標庫

這步驟是把 `noreply.pub` 新增至目標庫的 `Settings/Deploy keys` 並將權限設為允許寫入

1. 複製 noreply.pub 內容
    ```
    $ cat ~/.ssh/noreply.pub
    // ssh-rsa AAAAB3Nz.......@users.noreply.github.com
    ```
2. 在你的目標庫下，點擊Settings ![Settings1](1650251777396.jpg)
3. 在左側邊欄中，點擊Deploy keys
4. 點擊 Add deploy key
5. 在 Key 欄位貼上 noreply.pub 的內容
6. 勾選 Allow write access
7. 點擊 Add key 

最終你會得到這樣的結果

![Result1](1650253565960.jpg)

## 安裝私鑰至來源庫

這步驟是把 `noreply` 新增至來源庫的 `Settings/Secrets` 以利自動佈署時取得權限

1. 複製 noreply 內容
    ```
    $ cat ~/.ssh/noreply
    // -----BEGIN OPENSSH PRIVATE KEY-----
    // ........
    // -----END OPENSSH PRIVATE KEY-----
    ```
2. 在你的來源庫下，點擊Settings ![Settings](1650251777396.jpg)
3. 在左側邊欄中，點擊 Secrets 再點擊 Actions
4. 點擊 New repository secret
5. 在 Name 欄位輸入 `DEPLOY_KEY` (必須是這個值)
6. 在 Value 欄位貼上 noreply 的內容
8. 點擊 Add secret

最終你會得到這樣的結果

 ![安裝私鑰至來源庫](1650253654099.jpg)

## 創建 Git Action

使用 Git Actions 偵測每當 main branch 更新時自動佈署到目標庫

在你的來源庫下，點擊Actions 再點擊 `set up a workflow yourself` (實際上它就是在你的來源庫創建一個yaml檔)  ![Actions](1650254142113.jpg)

在 `Edit new file` 裡輸入以下內容

```
name: build
on:
push:
    branches: [ main ]
jobs:
build:
    runs-on: ubuntu-latest

    steps:
    - name: 'Building...'
    uses: reuixiy/hugo-deploy@v1
    env:
        DEPLOY_REPO: {username}/{username}.github.io
        DEPLOY_BRANCH: {branch name}
        DEPLOY_KEY: ${{ secrets.DEPLOY_KEY }}
        TZ: Asia/Taipei
```

- 記得將 `{username}` 改為你的帳戶名稱
- 記得將 `{branch name}` 改為主要的分支名稱，目前 github 政策是 `main`

然後點擊右上角 `Start commit` 就會開始執行第一次佈署

![Result](1650255112373.jpg)

這就是所有過程了，如果還有不了解的地方，你可以點擊右上角 `Gather虛擬辦公室` 試著找到我，恭喜你又學會了一件事

---

## 聽說：小故事大道理

來源 一人企業：一個人也能賺錢的商業新模式

幾年前，一款社交軟件Buffer，曾經瘋狂招聘員工，因為它希望大規模融資。當時企業對雇傭更多人，從而佔據更多市場份額、實現更大收益、給投資者一個滿意的答案這些事並沒有明確的想法，Buffer雇傭的員工數量超出了它的供養能力範圍。

隨後，危機出現了：Buffer的領導層意識到它就算接受外部融資，仍然需要裁掉11%的員工。問題出在哪兒了呢？

Buffer的領導團隊有分歧：COO（首席運營官）和CTO（首席技術官）更傾向於追逐高風險和高增長，也就是典型的初創企業所走的路線。他們認為應該根據營業收入目標招聘員工。但Buffer的CEO更希望制訂一個緩慢發展的計劃，這個計劃是利潤驅動的，認為企業只有積累了足夠的資金，才能雇傭更多員工。

最後，追求高風險高增長的領導層離開了企業。其他員工沒有離職或被解雇，留下來的人都認同CEO的緩慢的、以利潤為基礎的增長計劃。Buffer目前擁有300多萬用戶，卻僅有72個員工。

對「一人企業」來說，要回答的問題永遠是「我要怎樣做才能讓我的企業變得更好」，而不是「我要怎樣做才能讓我的企業變大」。
