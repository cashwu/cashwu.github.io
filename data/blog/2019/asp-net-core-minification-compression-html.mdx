---
title: ASP.NET Core 最小化和壓縮 HTML 輸出
summary: ASP.NET Core 最小化和壓縮 HTML 輸出
date: 2019-04-26 11:52:52.695+08:00
tags: [ asp.net core , html ]
draft: false
---

一般而言，頁面的大小跟載入速度有很大的關係，我們來看如何在 ASP.NET Core 最小化和壓縮 HTML 輸出

## 安裝套件

如果是 ASP.NET Core 2.X 的版本需要安裝 [`WebMarkupMin.AspNetCore2`](https://www.nuget.org/packages/WebMarkupMin.AspNetCore2/) 套件，1.X 的話需要安裝 [`WebMarkupMin.AspNetCore1`](https://www.nuget.org/packages/WebMarkupMin.AspNetCore1/)

## 最小化 HTML

- 在 `Startup` 裡面的 `ConfigureServices` 加入 `AddWebMarkupMin`，設定 `AllowMinificationInDevelopmentEnvironment` 為 `true`，可以在開發階段就看到最小化

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddWebMarkupMin(options =>
            {
                options.AllowMinificationInDevelopmentEnvironment = true;
            });
}
```

- 加入 `AddHtmlMinification`，設定 `MinificationSettings.WhitespaceMinificationMode`，可以把移除空白

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddWebMarkupMin(options =>
            {
                options.AllowMinificationInDevelopmentEnvironment = true;
            })
            .AddHtmlMinification(options =>
            {
                options.MinificationSettings.WhitespaceMinificationMode = WhitespaceMinificationMode.Safe;
            });
}
```

- 而且移除空白有不同的層級，建議使用 `WhitespaceMinificationMode.Safe` 選項

![](/static/images/404.webp)

- 在 `Startup` 裡面的 `Configure` 去使用 `UseWebMarkupMin`

```csharp
public void Configure(IApplicationBuilder app, IHostingEnvironment env)
{
    app.UseWebMarkupMin();
}
```

## 測試最小化 HTML

- 下面是原始沒有移除空白的原始碼和大小

![](/static/images/404.webp)

![](/static/images/404.webp)

- 加入 Minification 之後的原始碼和大小

![](/static/images/404.webp)

![](/static/images/404.webp)

## 壓縮 HTML

- 修改 `AddWebMarkupMin` 的設定，加入 `AllowCompressionInDevelopmentEnvironment`為 `true`，可以在開發階段就看到壓縮

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddWebMarkupMin(options =>
            {
                options.AllowMinificationInDevelopmentEnvironment = true;
				options.AllowCompressionInDevelopmentEnvironment = true;
            })
}
```

- 加入 `AddHttpCompression`，設定 `CompressorFactories` 為 `GZipCompressorFactory`

```csharp
services.AddWebMarkupMin(options =>
        {
            options.AllowMinificationInDevelopmentEnvironment = true;
            options.AllowCompressionInDevelopmentEnvironment = true;
        })
        .AddHtmlMinification(options =>
        {
            options.MinificationSettings.WhitespaceMinificationMode = WhitespaceMinificationMode.Safe;
        })
        .AddHttpCompression(options =>
        {
            options.CompressorFactories = new List<ICompressorFactory>
            {
                new GZipCompressorFactory()
            };
        });
```

## 測試壓縮 HTML

- 可以看到網頁的 `Content-Encoding` 變成 `gzip` 了

![](/static/images/404.webp)

## 後記

可以看到啟用最小化之後的大小從 `2.3KB` 變成 `1.7KB`，啟用壓縮之後又變成 `993B`，一整個就是差很多，建議可以啟用最小化加上壓縮，不過要注意的是，啟用壓縮之後會耗 server 的運算，而且 server 上還需要其它的設定才可以啟用