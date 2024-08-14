---
title: ASP.NET Core 專案加入方案檔
description: 如果用 ASP.NET Core CLI 建立的專案會只有專案檔而沒有方案檔，這跟我們在使用 IDE 工具 (Rider、VS) 建立出來的不太一樣，下面就來看怎麼使用 CLI 建立方案檔
date: 2018-12-22 16:42:12.402+08:00
slug: "asp-net-core-project-add-solution-file"
tags: [ asp.net core ]
---

如果用 ASP.NET Core CLI 建立的專案會只有專案檔而沒有方案檔，這跟我們在使用 IDE 工具 (Rider、VS) 建立出來的不太一樣，下面就來看怎麼使用 CLI 建立方案檔

- 先建立一個 API 專案 `dotnet new api -o api`
- 建立完成後會看到只有建立一層的資料夾和一個專案檔

![](/images/404.webp)

- 結構如下

![](/images/404.webp)

- 多建立一層資料夾 api，然後把原本的 api 搬進去，結構如下

![](/images/404.webp)

- 進到第一階的 api 資料夾，建立方案檔 `dotnet new sln`
- 把專案加入到方案裡面 `dotnet sln add ./api/api.csproj`

![](/images/404.webp)

- 如果查看方案檔的話就會看到有加入了一個 api 專案

![](/images/404.webp)