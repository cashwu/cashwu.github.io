---
title: ASP.NET Core 使用 ActionFilter 實作快取
summary: ASP.NET Core 使用 ActionFilter 來實作快取
date: 2019-04-17 10:30:37.33+08:00
tags: [ actionfilter , aop , asp.net core ]
draft: false
---

- 建立一個 `CacheActionFilter` class，實作 `Attribute` 和 `IAsyncActionFilter`

```csharp
public class CacheActionFilter : Attribute, IAsyncActionFilter
{
    public async Task OnActionExecutionAsync(ActionExecutingContext context, ActionExecutionDelegate next)
    {
		await next();
    }
}
```

- 可以拿到傳入 action 的參數和它的名稱當成快取的 key

```csharp
public class CacheActionFilter : Attribute, IAsyncActionFilter
{
    public async Task OnActionExecutionAsync(ActionExecutingContext context, ActionExecutionDelegate next)
    {
		var args = context.ActionArguments.Select(a => $"{JsonConvert.SerializeObject(a.Value)}");
        var arg = string.Join(",", args);
        var cacheKey = $"{context.ActionDescriptor.DisplayName}-{arg}";

		await next();
    }
}
```

- 可以拿到 response 之後使用 `MemoryCache` 快取起來
	- 這裡假設 API 的返回都只有 `OKObjectResut`
	- 為了之後方便使用，`IMemoryCache` 直接從 `RequestServices` 拿

```csharp
public class CacheActionFilter : Attribute, IAsyncActionFilter
{
    public async Task OnActionExecutionAsync(ActionExecutingContext context, ActionExecutionDelegate next)
    {
		var args = context.ActionArguments.Select(a => $"{JsonConvert.SerializeObject(a.Value)}");
        var arg = string.Join(",", args);
        var cacheKey = $"{context.ActionDescriptor.DisplayName}-{arg}";

		await next();
		if (response.Result is OkObjectResult result)
		{
			var memory = response.HttpContext.RequestServices.GetService<IMemoryCache>();
			memory.Set(cacheKey, result.Value);
		}
    }
}
```

- 使用 `MemoryCache` 要記得在 `startup` 註冊

```csharp
public void ConfigureServices(IServiceCollection services)
{
	services.AddMvc().SetCompatibilityVersion(CompatibilityVersion.Version_2_2);
    services.AddMemoryCache();
}
```

- 因為已經有把 response 快取了，所以可以在執行 `next` 之前判斷，如果有快取就直接返回快取，沒有的話就再執行 `next`

```csharp
public class CacheActionFilter : Attribute, IAsyncActionFilter
{
    public async Task OnActionExecutionAsync(ActionExecutingContext context, ActionExecutionDelegate next)
    {
		var args = context.ActionArguments.Select(a => $"{JsonConvert.SerializeObject(a.Value)}");
		var arg = string.Join(",", args);
		var cacheKey = $"{context.ActionDescriptor.DisplayName}-{arg}";

		var memoryCache = context.HttpContext.RequestServices.GetService<IMemoryCache>();

		if (memoryCache.TryGetValue(cacheKey, out object cacheResult))
		{
			context.Result = new OkObjectResult(cacheResult);
			return;
		}

		var response = await next();

		if (response.Result is OkObjectResult result)
		{
			memoryCache.Set(cacheKey, result.Value);
		}
    }
}
```

- 因為現在是有快取就不執行，應該是有點奇怪，應該要改成由外面決定快取的時間，如果超過一定的時間，還是要執行會比較合理

```csharp
public class CacheActionFilter : Attribute, IAsyncActionFilter
{
	private readonly int _duration;
	public CacheActionFilter(int duration)
	{
		_duration = duration;
	}

    public async Task OnActionExecutionAsync(ActionExecutingContext context, ActionExecutionDelegate next)
    {
		var args = context.ActionArguments.Select(a => $"{JsonConvert.SerializeObject(a.Value)}");
		var arg = string.Join(",", args);
		var cacheKey = $"{context.ActionDescriptor.DisplayName}-{arg}";

		var memoryCache = context.HttpContext.RequestServices.GetService<IMemoryCache>();

		if (memoryCache.TryGetValue(cacheKey, out object cacheResult))
		{
			context.Result = new OkObjectResult(cacheResult);
			return;
		}

		var response = await next();

		if (response.Result is OkObjectResult result)
		{
			memoryCache.Set(cacheKey, result.Value, TimeSpan.FromSeconds(_duration));
		}
    }
}
```

- 實際測試使用，一直 refresh 的話，時間每隔 5 秒才會變

```csharp
[HttpGet]
[CacheActionFilter(5)]
public ActionResult<string> Get(string name)
{
    return Ok($"{name} - {DateTime.Now.ToString()}");
}
```

![](/static/images/404.webp)