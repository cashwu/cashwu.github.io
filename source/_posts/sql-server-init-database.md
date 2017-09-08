---
title: SQL Server 正在啟動資料庫
tags:
  - sql
categories: []
date: 2017-06-01 10:14:44
---

## 問題

在 windows 的事件裡面一直出現 `正在啟動資料庫 Adventure Works2012`

![](./sql-server-init-database/01.png)

## 解法

```sql
ALTER DATABASE AdventureWorks2012
SET AUTO_CLOSE OFF
```
 
![](./sql-server-init-database/01.png)


### 參考連結

http://sharedderrick.blogspot.tw/2009/02/autoclose.html  