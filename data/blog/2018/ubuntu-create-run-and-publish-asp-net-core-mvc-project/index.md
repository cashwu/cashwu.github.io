---
title: Ubuntu - 建立、執行和發佈 ASP.NET Core MVC 專案
description: Ubuntu 建立、執行和發佈 ASP.NET Core MVC 專案
date: 2018-12-11 16:15:48.396+08:00
slug: "ubuntu-create-run-and-publish-asp-net-core-mvc-project"
tags: [ ubuntu , asp.net core ]
---

在[上一篇文章](https://blog.cashwu.com/blog/ubuntu-install-uninstall-net-core-sdk)，安裝完 .NET Core SDK 之後就可以來建立相關的網站

> OS - Ubuntu Desktop 18.04
> ASP.NET Core MVC 2.2

- 可以使用 `dotnet new -l` 來看現有的專案範本

![](/images/404.webp)

- 建立一個 MVC 的 Web App，放在 mvc 的資料夾裡面

```shell
donte new mvc -o mvc
```

![](/images/404.webp)

- 使用 `dotnet build` 來建置專案，會產生等一下要執行的 dll 檔 

![](/images/404.webp)

- 使用 `dotnet run` 來執行建置出來的 dll，基本上可以看到 `Application started.` 就是執行成功了

```shell
dotnet run ./bin/Debug/netcoreapp2.2/mvc.dll
```

![](/images/404.webp)

- 使用 `dotnet publish` 來發行 Web App，並且指定相關的 Configuration 和 runtime，預設是發行到 `bin` 下面的資料夾

```shell
dotnet publish -c Release -r ubuntu.18.04-x64
```

![](/images/404.webp)

- 需要注意的是，發佈出來的路徑是在 run times (這裡是 `ubuntu 18.04-x64`) 裡面的 publish 才是

![](/images/404.webp)

> 後面的文章會把 ASP.NET Core MVC 發佈出來的檔案用 nginx 來作反向代理