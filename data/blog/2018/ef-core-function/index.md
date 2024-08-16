---
title: EF Core - 呼叫 Function
summary: 如何在 EF Core 裡面去呼叫 Function
date: 2018-12-20 10:57:06.143+08:00
tags: [ ef core ]
draft: false
---

如何在 EF Core 裡面去呼叫 Function

> EF Core 2.2

## Table & Function

- 在 DB 裡面有兩個 Table 和一個 Function

```sql
CREATE TABLE [Test]
(
  Id     int ,
  Name   nvarchar(50)
)
GO

CREATE TABLE [User]
(
  Id     int ,
  Name   nvarchar(50)
)
GO

CREATE FUNCTION fn_Join (@id int)
  RETURNS TABLE
    AS
    RETURN
    (
      SELECT u.Name as UserName, t.Name as TestName
      FROM [Test] t
      join [User] u on t.Id = u.Id
      WHERE u.Id = @id
    );
GO
```

- DB 執行 Function 結果

![](/static/images/404.webp)

## 設定 DbContext

- 建立 Function 返回 Table 的型別

```csharp
public class JoinData
{
	public string UserName { get; set; }

	public string TestName { get; set; }
}
```

- 設定型別為 DbQuery

```csharp
public class AppDbContext : DbContext
{
    public AppDbContext(DbContextOptions<AppDbContext> options)
            : base(options)
    {
    }

    public DbQuery<JoinData> JoinData { get; set; }
}
```

## Query Function

- 使用 FromSql 來呼叫 Function

```csharp
var id = 1;
var data = _dbContext.JoinData.FromSql($"select * from fn_Join({id})").ToList();
```

- 結果

![](/static/images/404.webp)

- 產生出來的 SQL Command

![](/static/images/404.webp)