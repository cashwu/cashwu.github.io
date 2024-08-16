---
title: ASP.NET Core MVC - 使用 Heroku 的 PostgreSQL
summary: 前面文章 [ASP.NET Core MVC + Heroku] 已經把 .NET Core MVC 的專案放到 Heroku 了，現在要使用它所提供的免費 PostgreSQL，雖然免費的限制資料數量為 10,000 筆，不過如果是小型專案的話基本上已經夠用了，可以看一下 Heroku 的[介紹]
date: 2018-12-13 22:02:48.207+08:00
tags: [ asp.net core , heroku , postgresql ]
draft: false
---

前面文章 [ASP.NET Core MVC + Heroku](https://blog.cashwu.com/blog/asp-net-core-mvc-publish-heroku) 已經把 .NET Core MVC 的專案放到 Heroku 了，現在要使用它所提供的免費 PostgreSQL，雖然免費的限制資料數量為 10,000 筆，不過如果是小型專案的話基本上已經夠用了，可以看一下 Heroku 的[介紹](https://elements.heroku.com/addons/heroku-postgresql)

## Heroku CLI 建立

- 先進到之前的專案資料夾，就可以使用 Heroku 的 cli 來建立 Database

```shell
heroku addons:create heroku-postgresql:hobby-dev
```

![](/static/images/404.webp)

- 建立完成之後可以看一下相關的資訊

```shell
heroku pg:info
```

![](/static/images/404.webp)

- 可以直接透過 cli 拿到相關的連線資料

```shell
heroku pg:credentials:url DATABASE
```

![](/static/images/404.webp)

## Heroku 畫面建立

- 來到 `Resources` Tab，在下方  `Add-ons` 的地方搜尋 `Postgres`，點 `Heroku Postgres` 安裝

![](/static/images/404.webp)

- 選擇  `Hobby Dev - Free` 然後按 `Provision`

![](/static/images/404.webp)

- 看到畫面下方出現 `Heroku Postgres :: Database` 就代表建立好了，可以點進去

![](/static/images/404.webp)

- 會另開新分頁顯示 Database 的相關資訊

![](/static/images/404.webp)

- 可以點 `Settings` Tab，點開 `View Credentials`，可以在下面看到相關的連線資訊

![](/static/images/404.webp)

## 使用 DataGrip 連接

- 按照前面畫面上的資料，依序填入

![](/static/images/404.webp)

- 點選  `Advanced` Tab，找到 `sslmode`，把 Value 改成 `require`

![](/static/images/404.webp)

- 回到 `General` Tab，點 `Test Connection` 應該會出現 `Successful`

![](/static/images/404.webp)

## 使用 ASP.NET Core MVC 連接

- 在這裡會使用到之前上傳到 Heroku 的專案，然後相關的使用方式也可以參考之前的文章 [ASP.NET Core MVC - EF Core 使用 PostgreSQL](https://blog.cashwu.com/blog/asp-net-core-mvc-ef-core-postgresql)，這邊只講不一樣的地方

- 在 `UseNpgsql` 裡面需要多一個參數 `OptionBuilder`，裡面需要呼叫 `RemoteCertificateValidationCallback` 然後直接回傳 `true`

```csharp
services.AddDbContext<AppDbContext>(options =>
{
	options.UseNpgsql(Configuration.GetConnectionString("DefaultConnection"), optionBuilder =>
	{
		optionBuilder.RemoteCertificateValidationCallback((sender, certificate, chain, errors) => true);
	});
});
```

- 在 Connection 的地方，最後需要多一個參數 `SslMode=Require;`，需要注意的是大小寫必需要一樣，不然會有問題

```json
{
	"ConnectionStrings": {
		"DefaultConnection": "Server=aws.com;Port=5432;Database=db;UID=user;PWD=password;SslMode=Require;"
	}
}
```