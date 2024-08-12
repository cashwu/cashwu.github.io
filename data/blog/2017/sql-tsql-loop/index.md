---
title: SQL - TSQL Loop
description: TSQL Loop
date: 2017-06-06 15:50:19.735+08:00
slug: "sql-tsql-loop"
tags: [ sql ]
---

有的時候會在 DB 裡面塞一些假資料或者要測試新增資料時常常用到類似程式 Loop 的寫法

```sql
DECLARE @max INT
SET @i = 0
SET @max = 100 -- 要產生幾筆資料

WHILE (@i < @max)   
BEGIN
   
    INSERT INTO #Table VALUES('T')

    --加 1
    Set @i = @i + 1
END
```
