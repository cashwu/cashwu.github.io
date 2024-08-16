---
title: EF Core 使用 PostgreSQL Jsonb 型別
summary: 前面的文章有大概介紹了 PostgreSQL Json 和 Jsonb 的不同，現在要來看如何在 EF Core 裡面使用 Jsonb
date: 2018-12-26 09:11:25.196+08:00
tags: [ ef core , postgresql ]
draft: false
---

前面的[文章](https://blog.cashwu.com/blog/postgresql-json-jsonb)有大概介紹了 PostgreSQL Json 和 Jsonb 的不同，現在要來看如何在 EF Core 裡面使用 Jsonb

> EF Core 2.2

## PostgreSQL

- 有一個 data 的 Table，`type` 和 `user` 為 `jsonb`

![](/static/images/404.webp)

> 欄位名叫 `user` 會跟內建的 `user` 相衝，在實務上使用的話應該避免

## 使用 string 對應

- 在 `DbContext` 裡面的 `OnModelCreating`，去作 mapping
	- 因為 PostgreSQL 預設都是小寫，所以把 Table 和 Column 都先 mapping 成小寫
	- 然後把 2 個 Column mapping 成 `jsonb`

```csharp
protected override void OnModelCreating(ModelBuilder modelBuilder)
{
    modelBuilder.Entity<Data>(build =>
    {
        build.ToTable("data");

        build.Property(a => a.Id)
             .HasColumnName("id");

        build.Property(a => a.Type)
             .HasColumnName("type")
             .HasColumnType("jsonb");

        build.Property(a => a.User)
             .HasColumnName("user")
             .HasColumnType("jsonb");
	}
}
```

- 對應到 DB 的 Data Type
	- 2 個 jsonb 的 Column 都為 string

```csharp
public class Data
{
	public int Id { get; set; }

	public string Type { get; set; }

	public string User { get; set; }
}
```

- 執行結果，把 DB 的資料變成 string 輸出了

![](/static/images/404.webp)

- 不過拿到字串的話，在程式還需要在轉換一次才方便使用，所以我們可以使用前面[文章](https://blog.cashwu.com/blog/ef-core-value-converter)有提過的 `Value Converter` 來 mapping 成強型別

## 使用強型別對應

- 修改 OnModelCreating 的 mapping
	- 增加 2 個 Column 的 Converter，使用 `Json.NET` 進行轉換

```csharp
protected override void OnModelCreating(ModelBuilder modelBuilder)
{
    modelBuilder.Entity<Data>(build =>
    {
        build.ToTable(nameof(Data).ToLower());

        build.Property(a => a.Id)
             .HasColumnName("id");

        build.Property(a => a.Type)
             .HasColumnName("type")
             .HasColumnType("jsonb")
             .HasConversion(b => JsonConvert.SerializeObject(b),
                            b => JsonConvert.DeserializeObject<string[]>(b));

        build.Property(a => a.User)
             .HasColumnName("user")
             .HasColumnType("jsonb")
             .HasConversion(b => JsonConvert.SerializeObject(b),
                            b => JsonConvert.DeserializeObject<User>(b));
    });
}
```

- 修改 Data Type
	- 把 2 個 Column 的型別變成強型別

```csharp
public class Data
{
    public int Id { get; set; }

    public string[] Type { get; set; }

    public User User { get; set; }
}

public class User
{
    public int Id { get; set; }

    public string Name { get; set; }
}
```

- 執行結果
	- 可以看到已經轉成強型別了

![](/static/images/404.webp)

## 同場加映，使用 Sql Command

- 原生 PostgreSQL 有很多操作 Jsonb 方便的用法，這裡就用一個簡單的範例
	- 可以直接 where jsonb 裡面物件的 id

```csharp
var id = "1";
var data = _dbContext.Data.FromSql($"select * from data where data.user->>'Id' = {id}").FirstOrDefault();
```

- 執行結果

![](/static/images/404.webp)

## 後記

- 在 DB 可以存 Json 的格式真的很方便，可以使用的場景變多了，而且 PostgreSQL 又提供了很多相關的函式，讓我們可以很容昜的使用它，有機會可以在來介紹一些內建的函式