---
title: ASP.NET Core 自定義 Middleware 實作全站 Exception 處理
description: ASP.NET Core 自定義 Middleware 實作全站 Exception 處理
date: 2019-04-25 13:50:24.093+08:00
draft: true
slug: "asp-net-core-custom-middleware-exception-handling"
tags: [ actionfilter , aop , asp.net core , exception ]
---

在之前的文章 ( [ASP.NET Core 使用內建的 ExceptionHandler Middleware 實作全站 Exception 處理](https://blog.cashwu.com/blog/asp-net-core-exceptionhandler-middleware-handler-exception) )，使用內建的 ExceptionHandler 來處理全站的 Exception，現在要來看如何自定義 Middleware 處理全站的 Exception

## 建立 Middleware 類別

- 建立 CashExceptionHandler 類別，裡面有一個 `InvokeAsync` 的方法，內容是去 invoke 在 constructor 傳入的 `RequestDelegate`，然後傳入方法參數 `HttpContext`，這就是一個 Middleware 的基本內容

```csharp
public class CashExceptionHandler
{
    private readonly RequestDelegate _next;

    public CashExceptionHandler(RequestDelegate next)
    {
        _next = next;
    }

    public async Task InvokeAsync(HttpContext context)
    {
        await _next(context);
    }
}
```

- 寫好之後可以在 `Startup` 裡面去使用它
	- 一樣要注意先後次序的問題，建議可以放在最上面

```csharp
public void Configure(IApplicationBuilder app, IHostingEnvironment env)
{
    app.UseMiddleware<CashExceptionHandler>();
}
```

## Catch Exception

- 修改 Invoke 方法，使用 `try catch`，把呼叫 `next` 給包起來

```csharp
public async Task InvokeAsync(HttpContext context)
{
    try
    {
        await _next(context);
    }
    catch (Exception ex)
    {
        Console.WriteLine(ex.Message);
    }
}
```

## 測試

- 在 Action 裡面直接 throw Exception

![](/images/404.webp)

- 網頁是空的，因為 Exception 已經被我們 catch 住了

![](/images/404.webp)

- Log 也有寫到 Console

![](/images/404.webp)

## 實作 Catch Exception 內容

- constructor 注入 `LoggerFactory`，然後修改 catch 的內容，先 log Exception，然後返回自定義的內容

```csharp
public class CashExceptionHandler
{
    private readonly RequestDelegate _next;
    private readonly ILoggerFactory _loggerFactory;

    public CashExceptionHandler(RequestDelegate next, ILoggerFactory loggerFactory)
    {
        _next = next;
        _loggerFactory = loggerFactory;
    }

    public async Task InvokeAsync(HttpContext context)
    {
        try
        {
            await _next(context);
        }
        catch (Exception ex)
        {
            var logger = _loggerFactory.CreateLogger("ExceptionHandler");
            logger.LogError(ex, ex.Message);

            context.Response.StatusCode = 500;
            var result = JsonConvert.SerializeObject(new { Result = "Error" });
            await context.Response.WriteAsync(result);
        }
    }
}
```

## 測試

- 畫面上返回的是我們自定義的內容

![](/images/404.webp)

- Log 也有寫到 Console

![](/images/404.webp)

## 後記

使用內建的 `UseExceptionHandler`，和`自定義的 Middleware`，各有優缺點，不過，如果今天丟出來的是自定義的 Exception，使用自定義的 Middleware，可以做到比較多的事情，而不會被內建的給侷限住