---
title: SQL Server - 正在啟動資料庫
description: windows 的事件裡面一直出現 正在啟動資料庫
date: 2017-06-01 17:18:58.149+08:00
slug: "sql-server-init-database"
tags: [  sql ]
---

## 問題

在 windows 的事件裡面一直出現 `正在啟動資料庫 Adventure Works2012`

![](/images/404.webp)

## 解法

```sql
ALTER DATABASE AdventureWorks2012
SET AUTO_CLOSE OFF
```

![](/images/404.webp)

### 參考連結

[http://sharedderrick.blogspot.tw/2009/02/autoclose.html](http://sharedderrick.blogspot.tw/2009/02/autoclose.html)