---
title: ASP.NET Core MVC + Vue
summary: 把 Vue 整合到 ASP.NET Core API 的專案裡面，執行 .NET Core 的時候就可以把 Vue 給叫起來，不用在下前端的指令
date: 2018-12-19 11:30:39.555+08:00
tags: [ asp.net core , vue ]
draft: false
---

把 Vue 整合到 ASP.NET Core MVC 的專案裡面，執行 .NET Core 的時候就可以把 Vue 給叫起來，不用在下前端的指令

> ASP.NET Core MVC 2.2
> Vue CLI 3.0.3

## 建立 ASP.NET Core MVC 專案

```shell
dotnet new webapi -o corevue
```

![](/static/images/404.webp)

> 這是用 `web` 或是 `webapi`，在 .NET Core 基本上是沒有什麼差別的

## 建立 Vue 專案

- 因為這裡是建立在同一個資料夾，所以 Vue 會問你說資料夾已經存在，你要怎麼處理，記得一定要選 `Merge`

```shell
vue core corevue
```

![](/static/images/404.webp)

- 使用預設值建立就好

![](/static/images/404.webp)

![](/static/images/404.webp)

## 安裝 Webpack 套件

- 這裡整合會使用到 Webpack 的 `HMR` 技術，所以需要安裝套件

```shell
cd corevue
npm install -D aspnet-webpack webpack-hot-middleware
```

## 新增 vue.config.js

- 因為我們用的是 ASP.NET HMR 的整合，不是使用原生的，所以把 output 指回到 ASP.NET Core 的 `wwwroot` 資料夾，並且移除原本的 `hmr`

```js
module.exports = {
    outputDir: 'wwwroot',
    baseUrl: "/",
    chainWebpack: config => {
        config.plugins.delete('hmr');
    }
}
```

## 修改 Startup.cs

- 在 `Configure` 的 IsDevelopment 區塊增加 `UseWebpackDevMiddleware`，並且把 Config 的路徑指向 Vue CLI 的 `webpack.config.js`

> 不同的 OS 在路徑上可能會有問題，需要注意 !

```csharp
if (env.IsDevelopment())
{
    app.UseDeveloperExceptionPage();

    app.UseWebpackDevMiddleware(new WebpackDevMiddlewareOptions
    {
        HotModuleReplacement = true,
        ConfigFile = Path.Combine(env.ContentRootPath, @"node_modules/@vue/cli-service/webpack.config.js")
    });
}
```

- 修改原本的 `app.UseMvc`，如果不是 `/api` 開頭的，就導向到 `Home/Index`

```csharp
app.UseMvc(routes =>
{
    routes.MapRoute(
        name: "default",
        template: "{controller=Home}/{action=Index}/{id?}");
});

app.MapWhen(x => !x.Request.Path.Value.StartsWith("/api"), builder =>
{
    builder.UseMvc(routes =>
    {
        routes.MapSpaFallbackRoute(
            name: "spa-fallback",
            defaults: new { controller = "Home", action = "Index" });
    });
});
```

> 因為這裡用的專案是 `api`，所以多加了判斷
> 為了測試方便，可以先註解掉 `app.UseHttpsRedirection();`

## 新增 HomeController

- 把執行的頁面指向 Vue 產生出來的 `index.html`

```csharp
using Microsoft.AspNetCore.Mvc;

namespace corevue.Controllers
{
    public class HomeController : Controller
    {
        public IActionResult Index()
        {
            return File("~/index.html", "text/html");
        }
    }
}
```

## 執行

- 可以看的出來在執行的時候會幫你執行 `webpack`

```shell
dotnet run
```

![](/static/images/404.webp)

- 打開 [`http://localhost:5000/`](http://localhost:5000/) 就可以看到畫面了

![](/static/images/404.webp)

- 連到預設的 [api](http://localhost:5000/api/values) 也沒有問題

![](/static/images/404.webp)

## 後記

用這個方式來開發 SPA 相對來說方便許多，而且也有 `Hot Reload`，不用一直在重 build。不過程式碼都混在一起了，所以在專案的結構上面就會比較 `髒` 一點，而且如果有分前後端在開發的話，這個方式不一定適合

- 專案的 Github 在這 [ASPNETCore_Vue](https://github.com/cashwu/ASPNETCore_Vue) 可以 Clone 下來就直接使用 XD