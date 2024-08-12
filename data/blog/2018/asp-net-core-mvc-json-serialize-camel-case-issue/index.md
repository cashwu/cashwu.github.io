---
title: ASP.NET Core MVC - Json 序列化大小寫問題
description: 在 ASP.NET Core MVC 裡面預設的 Json 序列化行為和 ASP.NET MVC 不一樣，會把首字母變成小寫
date: 2018-12-18 18:56:03.735+08:00
slug: "asp-net-core-mvc-json-serialize-camel-case-issue"
tags: [ asp.net core ]
---

在 ASP.NET Core MVC 裡面預設的 Json 序列化行為和 ASP.NET MVC 不一樣，會把首字母變成小寫

- Action 程式碼如下

```csharp
public IActionResult Json()
{
    var data = new
    {
        Id = 1,
        Name = "Cash",
        TestData = "data"
    };

    return Json(new { Data = data });
}
```

- 執行結果

![](/images/404.webp)

- 如果調整的跟後端一樣的話，可以在 `Startup` 的 `ConfigureServices` 加一段 Json 的設定

```csharp
services.AddMvc()
    .AddJsonOptions(options =>
    {
        options.SerializerSettings.ContractResolver = new DefaultContractResolver();
    })
    .SetCompatibilityVersion(CompatibilityVersion.Version_2_2);
```

- 在一次執行，就可以看到大小寫和後端的是一樣的

![](/images/404.webp)