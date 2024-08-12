---
title: ASP.NET Core 使用內建的 ExceptionHandler Middleware 實作全站 Exception 處理
description: ASP.NET Core 使用內建的 ExceptionHandler Middleware 實作全站 Exception 處理
date: 2019-04-24 09:47:25.236+08:00
slug: "asp-net-core-exceptionhandler-middleware-handler-exception"
tags: [ aop , asp.net core , exception , middleware ]
---

要實作全站的 Exception Handler 的話，內建的 `Middleware` 有一個 `UseExceptionHandler` 可以使用，而且可以在 `ExceptionHandlerOptions` 裡面寫我們需要 Handler 的邏輯

## 實作 UseExceptionHandler

- 在 `Configure` 裡面會有執行先後次序的問題，如果是 `UseExceptionHandler` 的話，建議放在最前面，這樣子才有辦法抓到後面 Middleware 的 exception

```csharp
public void Configure(IApplicationBuilder app, ILogger logger)
{
    app.UseExceptionHandler(new ExceptionHandlerOptions());

    app.UseMvc(routes =>
    {
        routes.MapRoute(name: "default",
                        template: "{controller=Home}/{action=Index}/{id?}");
    });
}
```

- `ExceptionHandlerOptions` 裡面只有兩個東西
	- 一個是 `ExceptionHandlingPath` 也就是出錯了要導到什麼路徑叫它處理
	- 一個是 `ExceptionHandler`，就是如何處理 Exception

- 我們可以從 `Features` 拿到 `IExceptionHandlerFeature`，這裡面有 Error 可以使用 (也就是補抓到的 `Exception` )，我們可以判斷如果它不是空的話，就寫一筆 Log，然後返回狀態碼 `500` 和和自定的內容

```csharp
public void Configure(IApplicationBuilder app, ILoggerFactory loggerFactory)
{
    app.UseExceptionHandler(new ExceptionHandlerOptions
    {
        ExceptionHandler = async context =>
        {
            var exceptionFeature = context.Features.Get<IExceptionHandlerFeature>();
            if (exceptionFeature?.Error != null)
            {
                var logger = loggerFactory.CreateLogger("ExceptionHandler");
                logger.LogError(exceptionFeature.Error, exceptionFeature.Error.Message);
            }

            context.Response.StatusCode = 500;
            var result = JsonConvert.SerializeObject(new { Result = "Error" });
            await context.Response.WriteAsync(result);
        }
    });
}
```

## 測試

- 在某個 Action 裡面直接 throw Exception

![](/images/404.webp)

- 實際執行 Action，可以看到畫面上返回的是我們自定義的內容

![](/images/404.webp)

- 然後 Status Code 是 `500`

![](/images/404.webp)

- Log 也有寫到 Console

![](/images/404.webp)

## 寫成 Extension

- 為了方便使用，我們可以把 UseExceptionHandler 的程式碼搬到 Extension 裡面

```csharp
public static class MiddlewareExtension
{
    public static void UseExceptionHandler(this IApplicationBuilder app, ILoggerFactory loggerFactory)
    {
        app.UseExceptionHandler(new ExceptionHandlerOptions
        {
            ExceptionHandler = async context =>
            {
                var exceptionFeature = context.Features.Get<IExceptionHandlerFeature>();
                if (exceptionFeature?.Error != null)
                {
                    var logger = loggerFactory.CreateLogger("ExceptionHandler");
                    logger.LogError(exceptionFeature.Error, exceptionFeature.Error.Message);
                }

                context.Response.StatusCode = 500;
                var result = JsonConvert.SerializeObject(new { Result = "Error" });
                await context.Response.WriteAsync(result);
            }
        });
    }
}
```

- 在使用的時候一行就可以解決了

```csharp
public void Configure(IApplicationBuilder app, ILoggerFactory loggerFactory)
{
    app.UseExceptionHandler(loggerFactory);
}
```