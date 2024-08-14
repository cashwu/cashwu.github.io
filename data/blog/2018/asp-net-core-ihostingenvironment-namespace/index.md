---
title: ASP.NET Core 不同命名空間的 IHostingEnvironment
description: ASP.NET Core 的 IHostingEnvironment 存在兩個不同的命名空間，Microsoft.AspNetCore.Hosting 和 Microsoft.Extensions.Hosting，這兩個有什麼不一樣呢？
date: 2018-12-28 11:25:39.552+08:00
slug: "asp-net-core-ihostingenvironment-namespace"
tags: [ asp.net core ]
---

ASP.NET Core 的 IHostingEnvironment 存在兩個不同的命名空間 `Microsoft.AspNetCore.Hosting`和`Microsoft.Extensions.Hosting`，這兩個有什麼不一樣呢 ?

## 注入時

- 如果沒有相關的 namespace，注入時會叫你選擇

![](/images/404.webp)

## Microsoft.AspNetCore.Hosting

- [Github 原始碼](https://github.com/aspnet/AspNetCore/blob/master/src/Hosting/Abstractions/src/IHostingEnvironment.cs)

- class 的 summary，`Provides information about the web hosting environment an application is running in.`

- 主要是針對 `Web` 服務，所以會比 `Extensions` 多出了 `WebRootPath` 和 `WebRootFileProvider`
	- 官方說明，[ASP.NET Core Web 主機](https://docs.microsoft.com/zh-tw/aspnet/core/fundamentals/host/web-host?view=aspnetcore-2.2#host-configuration-values)

## Microsoft.Extensions.Hosting

- [Github 原始碼](https://github.com/aspnet/Extensions/blob/master/src/Hosting/Abstractions/src/IHostingEnvironment.cs)

- class 的 summary，`Provides information about the hosting environment an application is running in.`

- 主要是針對 `非Web` 服務
	- 官方說明，[.NET 泛型主機](https://docs.microsoft.com/zh-tw/aspnet/core/fundamentals/host/generic-host?view=aspnetcore-2.2#introduction)

## 後記

- 每次在注入，總是選擇 namespace，一直以來都是剛好猜中 `Microsoft.AspNetCore.Hosting` XD，現在總算搞清楚這兩個的差別了