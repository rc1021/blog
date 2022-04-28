---
title: "[Solve] Composer Without SSL"
date: 2022-04-18T19:35:44+08:00
tags: []
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

安裝 php composer 少數人會遇到的冷門問題

```
[Composer\Downloader\TransportException]                                                                                                   
  curl error 60 while downloading https://repo.packagist.org/packages.json: SSL certificate problem: unable to get local issuer certificate
```

這說明系統的憑證失效了。

有解法，可以繞過檢查，但我認為這麼做不明智。

```
$ composer config --global disable-tls true
$ composer config --global secure-http false
$ composer config --global repo.packagist composer http://packagist.org
```

小心用吧(如果不是你的系統別亂裝)，恭喜你節省了大約 20 分鐘

---

## 聽說：小故事大道理

有破釜沈舟死戰的決心，不等於去冒險。冒險是一件容易的事情，你把錢都壓到賭場上就是冒險，但是冒險和成功沒有必然的聯繫。


