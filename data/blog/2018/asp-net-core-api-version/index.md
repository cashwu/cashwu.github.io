---
title: 為你的 ASP.NET Core API 加上版本吧 !!
summary: 是不是有對外服務的 API 沒有辦法改版，怕改了就會有問題而影響到使用者，如果可以控制 API 的版本就沒有這個問題了，來為你的 API 加上版本吧 !!
date: 2018-12-21 22:23:26.624+08:00
tags: [ asp.net core , api ]
draft: false
---

是不是有對外服務的 API 沒有辦法改版，怕改了就會有問題而影響到使用者，如果可以控制 API 的版本就沒有這個問題了，來為你的 API 加上版本吧 !!

> ASP.NET Core 2.1.5

## 安裝套件

- 用 nuget 安裝 [Microsoft.AspNetCore.Mvc.Versioning](https://www.nuget.org/packages/microsoft.aspnetcore.mvc.versioning/)，目前的最新版為 3.0.0，此版本目前還不支援 `ASP.NET Core 2.2`

## 設定

- 在 `Startup` 的 Services 裡面註冊使用 `ApiVersioning`
	- ReportApiVersions 指的是會在 Header 裡面列出目前有的 Version
	- AssumeDefaultVersionWhenUnspecified 指的是可以不傳 Version，就會使用預設的 Version，也就是 DefaultApiVersion 的設定

```csharp
services.AddApiVersioning(o =>
{
    o.ReportApiVersions = true;
    o.AssumeDefaultVersionWhenUnspecified = true;
    o.DefaultApiVersion = new ApiVersion(1, 0);
});
```

## 預設 Version

- 加入兩個 Controller，`Value1Controller` 和 `Value2Controller`，把 Route 設定成一樣都是 `api/values`
- 在 Controller 上面加 `ApiVersion` attribute，指定每一個 Controller 的版本

```csharp
[ApiVersion("1.0")]
[Route("api/values")]
public class Value1Controller : ControllerBase
{
    [HttpGet]
    public string Get()
    {
        return "Version1";
    }
}
```

```csharp
[ApiVersion("2.0")]
[Route("api/values")]
public class Value2Controller : ControllerBase
{
    [HttpGet]
    public string Get()
    {
        return "Version2";
    }
}
```

- 因為有預設值的設定，所以如果瀏覽 `api/values` 時，都會進到 `Value1Controller` 裡面

![](/static/images/404.webp)

- 因為有設定 `ReportApiVersions`，所以看 Response 的 Header 就會看到有 `api-supported-versions`

![](/static/images/404.webp)

## 路由 Version

- 修改 `Value1Controller` 和 `Value2Controller` 的 `Route` 設定，把 `Version` 加入路由约束

```csharp
[ApiVersion("1.0")]
[Route("api/{v:apiVersion}/values")]
public class Value1Controller : ControllerBase
{
}
```

```csharp
[ApiVersion("2.0")]
[Route("api/{v:apiVersion}/values")]
public class Value2Controller : ControllerBase
{
}
```

- 修改後原本的路由就沒有用了，需要多傳 Version，這樣子就可以作到控制版本了

![](/static/images/404.webp)

## 淘汰 Version

- 如果有舊的版本預計要淘汰的話，可以多加上 `Deprecated` 的設定

```csharp
[ApiVersion("1.0", Deprecated = true)]
[Route("api/{v:apiVersion}/values")]
public class Value1Controller : ControllerBase
{
}
```

- 這樣子不管是用 1.0 還是 2.0，都會出現 `api-deprecated-versions` 和 `api-supported-versions` 跟你說目前的版本和要棄用的版本

![](/static/images/404.webp)