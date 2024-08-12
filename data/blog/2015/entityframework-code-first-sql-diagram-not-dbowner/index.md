---
title: EntityFramework - Code First 產生 DB 在建立 Diagram 時發生沒有有效的擁有者問題
description: EntityFramework Code First 產生 DB 在建立 Diagram 時發生沒有有效的擁有者問題
date: 2015-07-14 21:47:16.249+08:00
slug: "entityframework-code-first-sql-diagram-not-dbowner"
tags: [ ef , sql ]
---

## 問題

使用 Code First 產生 DB 後，要建立資料庫圖表時會出現訊息說沒有 `有效的擁有者`

![](/images/404.webp)

## 解法

- DB 上面按右鍵選擇 `屬性`

![](/images/404.webp)

- 在 `檔案` 裡面的 `擁有者` 選擇一個 DB 的登入者

![](/images/404.webp)

- 再一次建立時就可以了

![](/images/404.webp)