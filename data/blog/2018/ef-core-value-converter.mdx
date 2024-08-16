---
title: EF Core - 2.1 Value Converter
summary: 在 EF Core 2.1 加入了 Value Converter，讓我們可以更清鬆的轉換資料庫的資料變成我們需要的格式
date: 2018-12-18 09:40:09.669+08:00
tags: [ ef core ]
draft: false
---

在 EF Core 2.1 加入了 Value Converter，讓我們可以更清鬆的轉換資料庫的資料變成我們需要的格式

## EF Core & Enum

- 在 EF 下面可以直接使用 Enum 來當成一個欄位，在 DB 會存 Enum 的值

```csharp
public enum EnumStatus
{
    None = 0,
    Open = 1,
    Close = 2
}

public class User
{
    public int Id { get; set; }

    public string Name { get; set; }

    public EnumStatus Status { get; set; }
}
```

- 從 migration 裡面也可以看到它的型態是 `int`

![](/static/images/404.webp)

## Conversion

- 2.1 有多了一個新的功能，可以方便的幫我們轉換進出 DB 的資料

- 在 `OnModelCreating` 裡面加入 `Property` 的 `HasConversion`，方式有兩個參數
	- 第一個參數是從程式碼存入到 DB 的轉換
	- 第二個參數是從 DB 拿出來到程式碼的轉換

```csharp
public class AppDbContext : DbContext
{
    public AppDbContext(DbContextOptions<AppDbContext> options)
            : base(options)
    {
    }

    public DbSet<User> User { get; set; }

    protected override void OnModelCreating(ModelBuilder modelBuilder)
    {
        modelBuilder.Entity<User>()
                    .Property(a => a.Status)
                    .HasConversion(e => e.ToString(),
                                        e => (EnumStatus)Enum.Parse(typeof(EnumStatus), e));
    }
}
```

- 在作一次 migration 的話可以看到型態變成 `string` 了

![](/static/images/404.webp)

## 資料庫的結果

- 如果我們去 update 一次 User 的資料

```csharp
var user = _dbContext.User.FirstOrDefault(a => a.Id == 1);
user.Status = EnumStatus.Open;
```

- 可以看到資料庫裡面的值變成了字串了，而程式碼這端用的還是原本的 `Enum`

![](/static/images/404.webp)

## ValueConverter 類別

- 如果有很多資料表都用到這個 Enum 時，可以用 `ValueConverter` 來實作
	- 第一個泛型的參數是 Property 的型別
	- 第二個泛型的參數是轉換進 DB 的型別

```csharp
var converterEnumStatus = new ValueConverter<EnumStatus, string>(
												e => e.ToString(),
												e => (EnumStatus)Enum.Parse(typeof(EnumStatus), e));

modelBuilder.Entity<User>()
            .Property(a => a.Status)
            .HasConversion(converterEnumStatus);
```

## EF Core 內建的 Converter

- 其實在 EF Core 裡面已經有內建一些常用的[轉換器](https://docs.microsoft.com/zh-tw/ef/core/modeling/value-conversions#built-in-converters)，可以先看一下有沒有合適的，如果沒有的話在自己客製

- 以範例來說已經有內建的了，我們可以改寫成

```csharp
var converterEnumStatus = new EnumToStringConverter<EnumStatus>();

modelBuilder.Entity<User>()
            .Property(a => a.Status)
            .HasConversion(converterEnumStatus);
```