---
title: EF Core Postgres Concurrency Checks
description: EF Core Postgres Concurrency Checks
date: 2019-04-28 15:00:04.248+08:00
slug: "asp-net-core-postgres-concurrency-checks"
tags: [ ef core , postgresql ]
---

在 SQL Server 為了防止 Concurrency 的問題，是在資料表裡面多加一個類似 timestamp 的欄位 (`rowversion `) 來解決，而在 Postgres 怎麼解決這個問題 ? 

Npgsql 的 document [Optimistic Concurrency and Concurrency Tokens](https://www.npgsql.org/efcore/miscellaneous.html?q=Concurrency#optimistic-concurrency-and-concurrency-tokens) 有說明，基本上 Postgres 沒有 `rowversion` 的機制，不過它有類似的 token 機制，使用上非常方便，只要在資料表設定的地方加上一個設定 `ForNpgsqlUseXminAsConcurrencyToken` 就好了

```csharp
protected override void OnConfiguring(DbContextOptionsBuilder optionsBuilder)
{
	modelBuilder.Entity<Blog>()
                .ForNpgsqlUseXminAsConcurrencyToken();
}
```