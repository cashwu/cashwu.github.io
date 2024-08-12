---
title: ASP.NET Core MVC - 使用 Html.Raw 在 Markdown 的程式碼區塊的問題
description: 如果使用 Html.Raw 輸出 markdown 的程式碼區塊時，有 <> 的話就會幫你在多輸出一個結尾的 tag
date: 2018-12-18 13:15:05.741+08:00
slug: "asp-net-core-mvc-html-raw-markdown-code-area-issus"
tags: [ asp.net core , markdown ]
---

如果使用 `Html.Raw` 輸出 markdown 的程式碼區塊時，有 `<>` 的話就會幫你在多輸出一個結尾的 tag

- 程式碼如下

![](/images/404.webp)

- Html Source Code

![](/images/404.webp)

- Html

![](/images/404.webp)