---
title: ASP.NET Core 的 生命周期 IApplicationLifetime
summary: 如果想要知道 ASP.NET Core 的啟動和關閉，內建的 IApplicationLifetime 提供給我們三個屬性可以使用
date: 2018-12-28 13:36:12.446+08:00
tags: [ asp.net core ]
draft: false
---


如果想要知道 ASP.NET Core 的啟動和關閉，內建的 IApplicationLifetime 提供給我們三個屬性可以使用

> ASP.NET Core 2.2

## 註冊

- 可以在 `Startup` 的 `Configure`，注入 `IApplicationLifetime`

```csharp
public void Configure(IApplicationBuilder app, IApplicationLifetime applicationLifetime)
{
    app.UseMvcWithDefaultRoute();
}
```

## 生命周期

- 總共有三個生命周期可以使用
	- ApplicationStarted，啟動完閉
	- ApplicationStopping，正在關閉
	- ApplicationStopped，已經關閉

- 使用 `Register` 就可以傳入一個 `Action`，作你想要作的事情

```csharp
public void Configure(IApplicationBuilder app, IApplicationLifetime applicationLifetime)
{
    applicationLifetime.ApplicationStarted.Register(() =>
    {
        Console.WriteLine("ApplicationStarted");
    });

    applicationLifetime.ApplicationStopping.Register(() =>
    {
        Console.WriteLine("ApplicationStopping");
    });

    applicationLifetime.ApplicationStopped.Register(() =>
    {
        Console.WriteLine("ApplicationStopped");
    });

    app.UseMvcWithDefaultRoute();
}
```

## 手動關閉程式

- `IApplicationLifetime` 裡面提供了一個方法 `StopApplication` 可以要求程式關閉

```csharp
applicationLifetime.StopApplication();
```

## 後記

- 之前一直想要知道在雲端上的 APP 什麼時候被重啟的，就在官方的[文件](https://docs.microsoft.com/zh-tw/aspnet/core/fundamentals/host/web-host?view=aspnetcore-2.2#iapplicationlifetime-interface)，找到這個 interface 可以使用