---
title: ASP.NET Core 2.2 新的 Endpoint Routing
summary: 在 ASP.NET Core 2.2 的版本，Endpoint Routing 的行為和之前的版本不太一樣，來看一下差異的部份
date: 2018-12-27 10:15:46.338+08:00
tags: [ asp.net core ]
draft: false
---

在 ASP.NET Core 2.2 的版本，Endpoint Routing 的行為和之前的版本不太一樣，來看一下差異的部份

## 設定

- 在 2.2 的版本，預設 `Endpoint Routing` 是啟用的，可以修改 MVC 的設定把它關掉

```csharp
services.AddMvc(options => options.EnableEndpointRouting = false)
        .SetCompatibilityVersion(CompatibilityVersion.Version_2_2);
```

## 測試的連結

- 下面會產生這個 About 的連結來當測試

![](/static/images/404.webp)

## 產生沒有參數的連結

- 有 Enpoint Routing
	- 以 `Action` nmae 產生連結

![](/static/images/404.webp)

- 沒有 Enpoint Routing
	- 保留傳入參數的大小寫

![](/static/images/404.webp)

## 產生不存在的連結

- 有 Enpoint Routing
	- 無法產生連結

![](/static/images/404.webp)

- 沒有 Enpoint Routing
	- 一樣產生連結

![](/static/images/404.webp)

## 產生非空參數的連結

- 有 Endpoint Routing
	- 無法產生連結

![](/static/images/404.webp)

- 沒有 Endpoint Routing
	- 一樣產生連結

![](/static/images/404.webp)

## 產生可為空參數的連結

- 不管有跟沒有 Endpoint Routing 的結果一樣
	- 以 `Action` name 產生連結

![](/static/images/404.webp)

## 後記

- 感覺上這個改變是為了不要產生錯誤的連結，不過如果不清楚的人可能會覺得為什麼行為和之前不一樣
- 有關於相關的改動可以參考官方文件 [Differences from earlier versions of routing](https://docs.microsoft.com/en-us/aspnet/core/fundamentals/routing?view=aspnetcore-2.2#differences-from-earlier-versions-of-routing)