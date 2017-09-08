---
title: SQL - TSQL Dealy
tags:
  - sql
categories: []
date: 2017-06-06 09:55:02
---

有的時候會在 DB 裡面模擬執行時執行時間過長的 Timeout
很類似 c# 的 sleep 或是 js 的 setTimeout

```sql
WAITFOR DELAY '00:00:01';   
```

參考連結

https://msdn.microsoft.com/zh-tw/library/ms187331.aspx 