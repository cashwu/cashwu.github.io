---
title: ASP.NET Core Razor 即時編譯 
description: 在 ASP.NET MVC 的年代，畫面 (Razor) 修改完之後，在瀏覽器重新整理就可以看到修改後的畫面，這種即時編譯的方式在 .NET Core 就直接拿掉了，如果需要這個功能的話，需要自行安裝套件就可以達到一樣的效果
date: 2020-09-08 09:37:30.456+08:00
slug: "asp-net-core-razor-runtimecompilation"
tags: [ asp.net core ]
---

在 ASP.NET MVC 的年代，畫面 (Razor) 修改完之後，在瀏覽器重新整理就可以看到修改後的畫面，這種即時編譯的方式在 .NET Core 就直接拿掉了，如果需要這個功能的話，需要自行安裝套件就可以達到一樣的效果

> 官方文件 [Razor ASP.NET Core 中的檔案編譯](https://docs.microsoft.com/zh-tw/aspnet/core/mvc/views/view-compilation?view=aspnetcore-3.1)，需要注意的是只有在 `3.1` 之後的版本才可以使用

- 用 nuget 安裝 [Microsoft.AspNetCore.Mvc.Razor.RuntimeCompilation](https://www.nuget.org/packages/Microsoft.AspNetCore.Mvc.Razor.RuntimeCompilation)
- 在程式碼設定

```csharp
public void ConfigureServices(IServiceCollection services)
{
	// MVC Razor
    services.AddControllersWithViews()
            .AddRazorRuntimeCompilation();

	// Razor Page
    services.AddRazorPages()
            .AddRazorRuntimeCompilation();
}
```

這樣子畫面就可以即時編譯了 !!
