---
title: ASP.NET Core 使用 MiniProfiler 監控網站效能
summary: 網站寫好之後總是覺得很慢，但是又不知道慢在那裡，你就需要有檢測的工具來幫你監控網站的效能，我們使用 MiniProfiler 這個套件可以簡單的來幫我們作到這件事情
date: 2019-01-10 10:09:11.187+08:00
tags: [ asp.net core , miniprofiler ]
draft: false
---

網站寫好之後總是覺得很慢，但是又不知道慢在那裡，你就需要有檢測的工具來幫你監控網站的效能，我們使用 MiniProfiler 這個套件可以簡單的來幫我們作到這件事情

> ASP.NET Core 2.2
> MiniProfiler 4.0.138

## 安裝

- 使用 Nuget 安裝三個套件
	- `MiniProfiler`
	- `MiniProfiler.AspNetCore.Mvc` (基本上安裝這個就有包含 `MiniProfiler` 了)
	- `MiniProfiler.EntityFrameworkCore`

## 設定

- 在 `Startup` 的 `ConfigureServices` 裡面加入 `MiniProfiler`
	- 在這裡只設定 `RouteBasePath` 指向到 `/profiler`

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddMiniProfiler(options =>
            {
                options.RouteBasePath = "/profiler";
            })
            .AddEntityFramework();
}
```

> 在這裡沒有設定安全性，所以所有知道網址的人都可以瀏覽，如果要在正式環境使用的話，需要在加上權限的設定

- 在 `Configure` 去使用它

```csharp
public void Configure(IApplicationBuilder app)
{
    app.UseMiniProfiler();
}
```

## 檢測 MVC

- Controller 程式碼如下

```csharp
public class HomeController : Controller
{
 	[HttpGet]
	public IActionResult Index()
	{
		return View();
	}
}
```

- 先瀏覽預設的首頁 (`Home/Index`)，在瀏覽頁面 `/profiler/results`，就可以看到相關的檢測數據，載入這個頁面總共花了 `307.5ms`
	- 前面的 `/profiler` 是自己設定的 `RouteBasePath`

![](/static/images/404.webp)

- 點 `more columns` 可以看到更多的欄位

![](/static/images/404.webp)

- 點 `show trivial` 可以看到無關緊要的載入項目 (應該是速度 `< 1ms`)

![](/static/images/404.webp)

## 檢測 EF Core

- 修改 Controller 程式碼加入呼叫 EF Core，修改後重新瀏覽網頁

```csharp
public class HomeController : Controller
{
    private readonly AppDbContext _dbContext;

    public HomeController(AppDbContext dbContext)
    {
        _dbContext = dbContext;
    }

 	[HttpGet]
	public IActionResult Index()
	{
		var users = _dbContext.User.ToList();
		return View();
	}
}
```

- 瀏覽頁面 `/profiler/results，就可以看到下面多了 SQL 的相關資訊
	- 上面的速度欄位會多一個 `sql` 的欄位顯示連線 SQL 的速度，而且也會跟你說 sql 佔了總時間的比例，以下面的圖來看就是 `47.6%`
	- 下面的 SQL 的相關資訊會有 Open、ExecuteReader、Close 的時間，而且也可以看到 EF Core 轉譯成 Sql Command 的結果

![](/static/images/404.webp)

## 檢測 Razor

- 在 `_ViewImports.cshtml` 加入 MiniProfiler 的 TagHelper

```csharp
@addTagHelper *, MiniProfiler.AspNetCore.Mvc
```

- 在 View 裡面加入程式碼，修改後重新瀏覽網頁
	- profile 裡面的 name 是呈現在 MiniProfiler 裡面的名稱，類似 Tag
	- 裡面使用 `Thread.Sleep` 模擬呼叫一段程式碼

```html
<profile name="View">
    @{
       Thread.Sleep(500);
    }
    <span>Hello Cash!</span>
</profile>
```

- 瀏覽頁面 `/profiler/results`，可以看到最下面多了一行 `View` 的時間，而且差不多是 `500ms`

![](/static/images/404.webp)

## 使用 MiniProfile 的 Step

- 修改 `Action` 的程式碼，修改後重新瀏覽網頁
	- 使用 `using` 包住要檢查的程式碼，using 裡面使用 `MiniProfiler.Current.Step` 方法，傳入一個 `name`，會呈現在 MiniProfiler 裡面的名稱，類似 Tag
	- 一樣使用 `Thread.Sleep` 模擬呼叫一段程式碼

```csharp
	[HttpGet]
	public IActionResult Index()
	{
		using (MiniProfiler.Current.Step("Test"))
		{
			Thread.Sleep(500);
		}

		using (MiniProfiler.Current.Step("SQL"))
		{
			var l = _dbContext.User.ToList();
		}

		return View();
	}
```

- 瀏覽頁面 `/profiler/results`，可以看到多出了 `Test` 和 `SQL` 的名稱在 Controller 下面，然後最後面 SQL 的時間已經從 Controller 移到 SQL

![](/static/images/404.webp)

## 把 Miniprofile 的資訊呈現在原畫面上

- 如果要一直瀏覽另外一個頁面看數據也很很麻煩，所以可以把數據呈現在原畫面上

- 修改 `_Layout.cshtml`，在 Body 結束前加上 MiniProfiler 的 Tag

```html
<mini-profiler />
```

- 重新瀏覽畫面時就會看到左上角出現了四個數字，它把主要階段的數字呈現在這裡

![](/static/images/404.webp)

- 每個數字都可以在點開，看到的其實就是另外一個頁面的內容把它整個整合在這裡

![](/static/images/404.webp)

## 檢測 API

- 其實 MAC 和 API 的使用方法都一樣，只差在沒有 `Razor` 的部份和資訊無法呈現在畫面上，直接補圖

![](/static/images/404.webp)

![](/static/images/404.webp)

## 後記

- 使用 MiniProfile 來看網站的效能真的很方便，可以知道每個階段的執行時間，針對不同的點去優化，也可以設定自己的 Step 方便分類和找出真正的效能問題在那裡
- 如果要在正式環境使用的話，必須要注意安全性的問題，在這裡沒有特別的介紹 