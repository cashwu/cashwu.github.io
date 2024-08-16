---
title: ASP.NET Core 使用 User Secret 保護機敏資料
summary: 雖然在 .NET Core 裡面使用 appsetting 分成不同的環境給不同的設定檔已經很方便了，不過在開發的階段，如果每一個人的 DB 連線是連到自己本機的 DB，又或者是有個人的機敏資料會在開發上使用時，使用 User Secret 的方式來儲存就很方便
date: 2018-12-22 09:50:18.4+08:00
tags: [ asp.net core ]
draft: false
---

雖然在 .NET Core 裡面使用 appsetting 分不同的環境已經很方便了，不過在開發的階段，如果每一個人的 DB 連線是連到自己本機的 DB，這樣子又很麻煩，又或者是有個人的機敏資料會在開發上使用時，使用 User Secret 的方式來儲存就很方便

> ASP.NET Core 2.2

> macOS


## 儲存位置

- 每一個 OS 的儲存位置不一樣，請參考官方[說明](https://docs.microsoft.com/zh-tw/aspnet/core/security/app-secrets?view=aspnetcore-2.1&tabs=macos)

- 可以直接進到資料夾看，每一個 `GUID` 代表的就是一個 APP，裡面其實是使用一個 `secrets.json` 來存資料，就像是 `appsetting.json` 一樣

![](/static/images/404.webp)

## 專案加入 User Secret

- 在專案檔裡面加上 `UserSecretsId`

![](/static/images/404.webp)

## 使用 Command Line 操作 User Secret

- 可以進到專案的資料夾使用 Command Line 來作操作 User Secret

- 列出目前的資料 `dotnet user-secrets list`

![](/static/images/404.webp)

- 新增一筆資料 `dotnet user-secrets set {Key} {Value}`

![](/static/images/404.webp)

- 刪除一筆資料 `dotnet user-secrets remove {Key}`

![](/static/images/404.webp)

## 儲存的資料

- 新增資料之後可以查看 APP 相對應的 `secrets.json`

![](/static/images/404.webp)

## 專案使用 User Secret

- 使用方法跟原本 appsetting 的使用方式一樣，DI 注入 `IConfiguration` 之後就可以使用 Key 拿到了

```csharp
private readonly IConfiguration _configuration;

public HomeController(IConfiguration configuration)
{
    _configuration = configuration;
}

public IActionResult Index()
{
    var secretKey = _configuration["SecretKey"];
    return View();
}
```

![](/static/images/404.webp)

- 如果要用強型別使用，請參考之前的文章 [ASP.NET Core MVC - 強型別 Configuration](https://blog.cashwu.com/blog/asp-net-core-mvc-strong-type-configuration)