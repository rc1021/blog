---
title: "MySQL 相關筆記"
date: 2022-04-30T21:01:06+08:00
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

## Q&A

### How to get size of mysql database?

```
    mysql> SELECT table_schema AS "Database", 
        ROUND(SUM(data_length + index_length) / 1024 / 1024, 2) AS "Size (MB)" 
        FROM information_schema.TABLES 
        GROUP BY table_schema;
+--------------------+-----------+
| Database           | Size (MB) |
+--------------------+-----------+
| default            |    106.97 |
+--------------------+-----------+
1 rows in set (0.26 sec)
```

cp -R /var/lib/mysql/* .

ubuntu@instance-1:~$ sudo service mysql stop
ubuntu@instance-1:~$ sudo service mysql status

