---
title: "Linux 硬碟空間相關指令"
date: 2022-04-30T10:11:18+08:00
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

- `du -sh {指定路徑}/* ` 列出指定路徑目錄大小
- `du -sh {指定路徑}/*  | sort -h` 排序、列出指定路徑目錄大小

ubuntu@instance-1:~$ sudo lsblk
NAME    MAJ:MIN RM   SIZE RO TYPE MOUNTPOINT
loop1     7:1    0   294M  1 loop /snap/google-cloud-sdk/235
loop2     7:2    0  55.5M  1 loop /snap/core18/2344
loop3     7:3    0 110.6M  1 loop /snap/core/12834
loop4     7:4    0 294.3M  1 loop /snap/google-cloud-sdk/237
loop5     7:5    0 111.6M  1 loop /snap/core/12941
loop6     7:6    0  55.5M  1 loop /snap/core18/2284
sda       8:0    0    60G  0 disk 
├─sda1    8:1    0  37.9G  0 part /
├─sda14   8:14   0     4M  0 part 
└─sda15   8:15   0   106M  0 part /boot/efi
sdb       8:16   0    35G  0 disk 



ubuntu@instance-1:~$ sudo df -Th
Filesystem     Type      Size  Used Avail Use% Mounted on
udev           devtmpfs  4.4G  4.4G     0 100% /dev
tmpfs          tmpfs     896M   32M  865M   4% /run
/dev/sda1      ext4       37G   37G     0 100% /
tmpfs          tmpfs     4.4G     0  4.4G   0% /dev/shm
tmpfs          tmpfs     5.0M     0  5.0M   0% /run/lock
tmpfs          tmpfs     4.4G     0  4.4G   0% /sys/fs/cgroup
/dev/sda15     vfat      105M  3.4M  102M   4% /boot/efi
/dev/loop6     squashfs   56M   56M     0 100% /snap/core18/2284
/dev/loop2     squashfs   56M   56M     0 100% /snap/core18/2344
/dev/loop5     squashfs  112M  112M     0 100% /snap/core/12941
/dev/loop3     squashfs  111M  111M     0 100% /snap/core/12834
/dev/loop1     squashfs  295M  295M     0 100% /snap/google-cloud-sdk/235
/dev/loop4     squashfs  295M  295M     0 100% /snap/google-cloud-sdk/237
tmpfs          tmpfs     896M     0  896M   0% /run/user/1000


執行命令

sudo apt-get update

出現錯誤E: Some index files failed to download, they have been ignored, or old ones used instead
可以將目錄下/var/lib/apt/lists/partial/所有的檔案清掉

$ sudo rm /var/lib/apt/lists/* -vf