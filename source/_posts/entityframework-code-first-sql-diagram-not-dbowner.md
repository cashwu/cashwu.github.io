---
title: EntityFramework Code First 產生 DB 在建立 Diagram 時發生沒有有效的擁有者問題
tags:
  - sql
  - ef
categories: []
date: 2015-07-14 08:00:00
---


## 問題

![](./entityframework-code-first-sql-diagram-not-dbowner/01.png)

使用 Code First 產生 DB 後，要建立資料庫圖表時會出現訊息說沒有 `有效的擁有者`

## 解法

- DB 上面按右鍵選擇 `屬性`

![](./entityframework-code-first-sql-diagram-not-dbowner/02.png)

- 在 `檔案` 裡面的 `擁有者` 選擇一個 DB 的登入者

![](./entityframework-code-first-sql-diagram-not-dbowner/03.png)

- 再一次建立時就可以了

![](./entityframework-code-first-sql-diagram-not-dbowner/04.png)