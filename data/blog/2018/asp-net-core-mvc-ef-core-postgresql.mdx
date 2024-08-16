---
title: ASP.NET Core MVC - EF Core 使用 PostgreSQL
summary: 在 ASP.NET Core MVC 搭配 EF Core 使用 Postgre SQL
date: 2018-12-13 15:00:59.79+08:00
tags: [ asp.net core , ef core , postgresql ]
draft: false
---

前面的文章 ([Ubuntu - 安裝 PostgreSQL](https://blog.cashwu.com/blog/ubuntu-install-postgresql)) 已經有建立好一個 PostgreSQL，現在要使用 ASP.NET Core MVC 的專案去連結這個 Database

> ASP.NET Core MVC 2.2

- 在  ASP.NET Core MVC 裡面要連結 PostgreSQL 需要使用第三方寫好的元件 [Npgsql](https://www.npgsql.org/)，而且也有支援在 EF Core 裡面使用

- 用 nuget 安裝套件
  - Npgsql.EntityFrameworkCore.PostgreSQL
  - Npgsql.EntityFrameworkCore.PostgreSQL.Design

- 建立 EF Core 的 AppDbContext，然後有一個 Table 為 User

```csharp
public class AppDbContext : DbContext
{
	public AppDbContext(DbContextOptions<AppDbContext> options)
		: base(options)
	{
	}

	public DbSet<User> User { get; set; }
}

public class User
{
	public int Id { get; set; }

	public string Name { get; set; }
}
```

- 註冊 AppDbContext 在 Startup.cs 的 ConfigureServices 裡面，options 裡面注意用的是 `UseNpgsql`

```csharp
// 為了方便省略了其它程式碼
public void ConfigureServices(IServiceCollection services)
{
	services.AddDbContext<AppDbContext>(options =>
	{
		options.UseNpgsql(Configuration.GetConnectionString("DefaultConnection"));
	});
}
```

- 新增一個 `DefaultConnection` 在 appsettings.json

```json
{
  "ConnectionStrings": {
    "DefaultConnection": "Server=10.211.55.15;Port=5432;Database=mvc;UID=mvc;PWD=mvc"
  }
}
```

- 使用 command 新增一個 EF 的 migrations

```shell
dotnet ef migrations add init
```

![](/static/images/404.webp)

- update migrations 到 Database

```shell
dotnet ef database update
```

![](/static/images/404.webp)

- 使用其它的 Client 端 (這裡用的是 DataGrip) 查看 Database，有多了兩張 Table

![](/static/images/404.webp)