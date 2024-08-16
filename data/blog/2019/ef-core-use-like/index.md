---
title: EF Core 使用 Like 查詢
summary: 如何在 EF Core 裡面使用 Like 作查詢
date: 2019-01-07 21:05:14.553+08:00
tags: [ ef core ]
draft: false
---

如何在 EF Core 裡面使用 Like 作查詢

> EF Core 2.2
> ASP.NET Core 2.2
> SQL Server 2017 on Linux

## 可用版本

在 EF Core 2.0 之後才支援使用 Like 查詢，([EF Core 2.0 中的新功能](https://docs.microsoft.com/zh-tw/ef/core/what-is-new/ef-core-2.0))

## 語法

- 使用 `EF.Functions.Like` 方法，第一個參數是欄位，第二個參數是比對的字串

```csharp
_dbContext.User.Where(a => EF.Functions.Like(a.Name, "bc%"));
_dbContext.User.Where(a => EF.Functions.Like(a.Name, "%bc"));
```

- 結果

![](/static/images/404.webp)

![](/static/images/404.webp)

## 後記

- 在 EF Core 2.0 之後有 `Like` 語法在某些特殊的場景還蠻有用的，不過還是要注意 `Index` 效能的問題
- `EF.Functions` 裡面也有一系列的日期方法可以用，有機會可以在來介紹