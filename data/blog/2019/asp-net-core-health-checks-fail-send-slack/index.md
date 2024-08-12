---
title: ASP.NET Core Health Checks 失敗時使用 Slack 通知
description: ASP.NET Core Health Checks 失敗時使用 Slack 通知
date: 2019-04-18 14:27:25.543+08:00
slug: "asp-net-core-health-checks-fail-send-slack"
tags: [ asp.net core ]
---

之前有寫過一篇文章 [ASP.NET Core MVC - 2.2 Health Checks](https://blog.cashwu.com/blog/asp-net-core-mvc-health-checks)，怎麼使用 2.2 的新功能 Health Check，現在要來加上 check 失敗時使用 Slack 通知

## 建立 Slack 的 Incoming Webhooks

先到自己的  Incoming Webhooks APP 頁面，網址是 `https://你的slack名.slack.com/apps/A0F7XDUAZ-incoming-webhooks`

![](/images/404.webp)

可以按左邊的 `Add Configuration` 建立一個新的設定，然後把 WebHook URL 記下來，等一下會使用到

![](/images/404.webp)

## 增加 Slack 設定

在原本 HealthChecks 的下面多一個 Webhooks 的設定，詳細的設定內容可以參考官方的[範本](https://github.com/Xabaril/AspNetCore.Diagnostics.HealthChecks/blob/master/doc/webhooks.md)，在這裡的設定都是以官方的範本為主

- `Uri` 是在前一個步驟拿到的 Webhook URL
- `Payload` 是失敗時送給 slack 的訊息
- `RestoredPayload` 是回狀態回覆時送給 slack 的訊息

```json
{
  "HealthChecks-UI": {
    "HealthChecks": [
      {
        "Name": "Cash Check",
        "Uri": "http://localhost:5000/checkui"
      }
    ],
    "Webhooks": [
      {
        "Name": "Slack",
        "Uri": "https://hooks.slack.com/services/",
        "Payload": "",
        "RestoredPayload": ""
      }
    ],
    "EvaluationTimeOnSeconds": 10
  }
}
```

## Statup 設定

Startup 的設定跟一篇一樣

```csharp
public void ConfigureServices(IServiceCollection services)
{
	services.AddMvc()
			.SetCompatibilityVersion(CompatibilityVersion.Version_2_2);

    services.AddHealthChecksUI()
            .AddHealthChecks()
            .AddNpgSql(Configuration.GetConnectionString("DefaultConnection"));
}

public void Configure(IApplicationBuilder app, IHostingEnvironment env)
{
    app.UseHealthChecks("/checkui", new HealthCheckOptions
    {
        Predicate = _ => true,
        ResponseWriter = UIResponseWriter.WriteHealthCheckUIResponse
    });
    app.UseHealthChecksUI(options =>
    {
        options.UIPath = "/CashCheck";
    });

    app.UseMvc();
}
```

## UI 的 Webhooks

如果設定檔沒有寫錯的話，在 UI 的 Webhooks 可以看到剛才寫在設定檔的內容

![](/images/404.webp)

## 測試

如果 Check 失敗時就會收到訊息

![](/images/404.webp)

狀態回復時也會收到訊息

![](/images/404.webp)