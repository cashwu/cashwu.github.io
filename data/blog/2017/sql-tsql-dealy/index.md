---
title: SQL - TSQL Delay
summary: TSQL Delay
date: 2017-06-07 14:48:19.869+08:00
tags: [ sql ]
draft: false
---

有的時候會在 DB 裡面模擬執行時執行時間過長的 Timeout
很類似 c# 的 sleep 或是 js 的 setTimeout

```sql
WAITFOR DELAY '00:00:01';   
```

### 參考連結

[官方說明 WAITFOR (Transact-SQL)](https://msdn.microsoft.com/zh-tw/library/ms187331.aspx)