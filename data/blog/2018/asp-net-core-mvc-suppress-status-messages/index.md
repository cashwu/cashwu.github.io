---
title: ASP.NET Core MVC - 取消執行時的狀態訊息
description: ASP.NET Core MVC 取消執行時的狀態訊息
date: 2018-12-18 09:24:41.851+08:00
slug: "asp-net-core-mvc-suppress-status-messages"
tags: [ asp.net core ]
---

- 在執行 .NET Core MVC 專案的時候都會有一段執行訊息 (如下圖)

![](/images/404.webp)

- 如果不想要有這段訊息的話，需要在 `Program` 裡面加上一段設定 `SuppressStatusMessages(true)`

```csharp
public static IWebHostBuilder CreateWebHostBuilder(string[] args)
{
    return WebHost.CreateDefaultBuilder(args)
                  .SuppressStatusMessages(true)
                  .UseStartup<Startup>();
}
```

- 再次執行的話，就不會出現了

![](/images/404.webp)