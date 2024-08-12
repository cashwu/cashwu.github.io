---
title: ASP.NET Core MVC - 強型別 Configuration
description: 在 ASP.NET Core MVC 裡面預設有讀取 Configuration 的機制，而如果沒有要使用到 IOption，其實可以把讀到的 Configuration 用強型別的方式注入到要使用的地方，會更加方便的使用
date: 2018-12-11 10:33:45.037+08:00
slug: "asp-net-core-mvc-strong-type-configuration"
tags: [ asp.net core ]
---

在 ASP.NET Core MVC 裡面預設有讀取 Configuration 的機制，而如果沒有要使用到 IOption，其實可以把讀到的 Configuration 用強型別的方式注入到要使用的地方，會更加方便的使用

- 有一個 Config 和相對應的類別

```json
{
	"TestConfig" : {
    	"Url" : "https://blog.cashwu.com"
  	}
}
```

```csharp
public class TestConfig
{
	public string Url { get; set; }
}
```

- 我們可以在 `Startup` 的地方，註冊這個 Config 並且對應到一個類別

```csharp
services.Configure<TestConfig>(Configuration.GetSection("TestConfig"));
```

- 在使用上就可以注入 `IOption<TestConfig>` 來使用，只不過還需要點 Value 一次才可以拿到實體的類別

```csharp
private readonly TestConfig _config;
public IndexModel(IOptions<TestConfig> config)
{
	_config = config.Value;
}
```

- 如果沒有要用到 IOption 的話，可以把注冊 Service 的地方再加一個註冊 IOption.Value 的類別，這樣子就可以直接注入類別使用

```csharp
services.Configure<TestConfig>(Configuration.GetSection("TestConfig"));
services.AddSingleton(r => r.GetRequiredService<IOptions<TestConfig>>().Value);
```

```csharp
private readonly TestConfig _config;
public IndexModel(TestConfig config)
{
	_config = config;
}
```

- 如果有很多 Config 都需要這樣子寫的話，可以寫一個共用的擴充方法來作這件事情，可以參考 Baymax 的 [Config](https://github.com/cashwu/Baymax#config)，程式碼在這 [`ConfigureServiceExtensions`](https://github.com/cashwu/Baymax/blob/master/Src/Baymax/Extension/ConfigureServiceExtensions.cs#L49)