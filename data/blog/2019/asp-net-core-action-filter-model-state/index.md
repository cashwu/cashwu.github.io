---
title: ASP.NET Core 使用 ActionFilter 驗證 ModelState
description: ASP.NET Core 使用 ActionFilter 來驗證 ModelState
date: 2019-04-17 09:00:18.862+08:00
slug: "asp-net-core-action-filter-model-state"
tags: [ actionfilter , aop , asp.net core ]
---

> 下面這個方法基本上只可以應用在 API 上面，如果是返回一個 View 時，可能就不適用

以往我們都會在 action 裡面驗證 `ModelState.IsValid`，所以每一個 action 裡面都會多出這一段代碼，其實可以寫一個 `ActionFilter` 使用 `AOP` 的方式把這一段代碼給抽離出去，這樣子之後就不用在 action 裡面去檢查 ModelState 了

```csharp
public IActionResult Index()
{
    if (!ModelState.IsValid)
    {
        return BadRequest();
    }
    return Ok("OK");
}

public IActionResult Contact()
{
    if (!ModelState.IsValid)
    {
        return BadRequest();
    }
    return Ok("OK");
}
```

- 先建立一個 `ModelStateValidActionFilter` class，讓它去實作 `IActionFilter`

```csharp
public class ModelStateValidActionFilter : IActionFilter
{
    public void OnActionExecuting(ActionExecutingContext context)
    {
    }

    public void OnActionExecuted(ActionExecutedContext context)
    {
    }
}
```

- 實作 `OnActionExecuting` 內容，最簡單的方式就是判斷 `IsValid` 就直接 return 掉，不是的話就回 `BadRequest`

```csharp
public class ModelStateActionFilter : IActionFilter
{
    public void OnActionExecuting(ActionExecutingContext context)
    {
		if (context.ModelState.IsValid)
		{
			return;
		}

		context.Result = new BadRequestResult();
    }

    public void OnActionExecuted(ActionExecutedContext context)
    {
    }
}
```

- 不過這樣子前端沒有辦法知道是什麼錯誤，我們可以自定一個回傳的型別來作這件事

```csharp
public class ResultDto<T> where T : class
{
    public IList<ErrorDto> Error { set; get; } = new List<ErrorDto>();

    public int Code { set; get; }

    public T Result { set; get; }
}

public class ErrorDto
{
    public string Message { set; get; }

    public string Field { set; get; }
}
```

- OnActionExecuting 修改成，先從 ModelState 把所有的錯誤和錯誤的欄位找出來，然後放到自定義的回傳型別，然後回傳

```csharp
public class ModelStateActionFilter : IActionFilter
{
    public void OnActionExecuting(ActionExecutingContext context)
    {
		if (context.ModelState.IsValid)
		{
			return;
		}

		var errors = context.ModelState
                    .SelectMany(modelState => modelState.Value.Errors
								.Select(a => new ErrorDto
								{
									Field = modelState.Key,
									Message = a.ErrorMessage
								}))
                    .ToList();

		var result = new ResultDto<dynamic>
		{
			Code = 400,
			Error = errors,
			Result = "The data is invalid"
		};

		context.Result = new OkObjectResult(result);
	}

    public void OnActionExecuted(ActionExecutedContext context)
    {
    }
}
```

- 在 startup 的 ConfigureServices 註冊到全站的 `Filters`

```csharp
services.AddMvc(options =>
		{
			options.Filters.Add<ModelStateValidActionFilter>();
		})
		.SetCompatibilityVersion(CompatibilityVersion.Version_2_2);
```

- 實際的執行結果

![](/images/404.webp)