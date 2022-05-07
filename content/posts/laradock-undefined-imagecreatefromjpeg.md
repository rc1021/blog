---
title: "Laradock-PHP-Worker Call to undefined function Intervention\\Image\\Gd\\imagecreatefromjpeg()"
date: 2022-05-06T23:54:02+08:00
tags: ['laradock', 'php-worker', 'gd', 'imagecreatefromjpeg']
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

## 結論寫在前面

移除 Laradock 在 php-worker Dockerfile(line:90) 的 `--with-png` 就能解決 `Call to undefined function Intervention\Image\Gd\imagecreatefromjpeg()` 的問題。

## 原因

PHP 7.4(Alpine) 安裝 `gd` 要獲得 JPEG 的支持，在編譯組態時加入 `--with-jpeg` 即可。**但是**! Laradock 在 php-worker Dockerfile(line:90) 裡**多**加入了 `--with-png` 導致編譯失敗。

## 修改 Dockerfile 重建 image

修改 php-worker 的 Dockerfile

```
// laradocker/php-worker/Dockerfile: 90
docker-php-ext-configure gd --with-freetype --with-jpeg --with-png; \
```

改為

```
docker-php-ext-configure gd --with-freetype --with-jpeg; \
```

然後，重新建立 image

```
$ docker-compose up --build -d php-worker
Recreating laradock_php-worker_1     ... done
```

檢查重建的環境是否支持 JPEG

```
$ docker exec -it laradock_php-worker_1 php -r 'print_r(gd_info());' 
Array
(
    [GD Version] => bundled (2.1.0 compatible)
    [FreeType Support] => 1
    [FreeType Linkage] => with freetype
    [GIF Read Support] => 1
    [GIF Create Support] => 1
    [JPEG Support] => 1        // good!
    [PNG Support] => 1
    [WBMP Support] => 1
    [XPM Support] => 
    [XBM Support] => 1
    [WebP Support] => 
    [BMP Support] => 1
    [TGA Read Support] => 1
    [JIS-mapped Japanese Font Support] => 
)
```

恭喜你又解決了一個問題

---

## 聽說：劃線筆記

來源 性格修正：如何突破你的原生性格

雖然你無法改變過去，但你可以改變的是，如何看待過去；造就你當下性格的，不是過往的經歷，而是你對經歷的看法。

