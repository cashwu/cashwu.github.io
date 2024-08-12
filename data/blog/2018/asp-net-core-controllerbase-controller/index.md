---
title: ASP.NET Core ControllerBase 和 Controller
description: ASP.NET Core 有兩個 Controller 可以繼承的父類別 ControllerBase 和 Controller，這兩個有什麼不同呢 ?
date: 2018-12-27 15:59:58.67+08:00
slug: "asp-net-core-controllerbase-controller"
tags: [ asp.net core ]
---

ASP.NET Core 有兩個 Controller 可以繼承的父類別 ControllerBase 和 Controller，這兩個有什麼不同呢 ?

## ControllerBase

- [Github 原始碼](https://github.com/aspnet/AspNetCore/blob/master/src/Mvc/src/Microsoft.AspNetCore.Mvc.Core/ControllerBase.cs)

- 所在的組件 `Microsoft.AspNetCore.Mvc.Core`

- class 的 summary `A base class for an MVC controller without view support.`
	- 它不支援 `View` 相關的東西，所以如果是寫 `API` 的話可以直接繼承它

## Controller

- [Github 原始碼](https://github.com/aspnet/AspNetCore/blob/master/src/Mvc/src/Microsoft.AspNetCore.Mvc.ViewFeatures/Controller.cs)

- 所在的組件 `Microsoft.AspNetCore.Mvc.ViewFeatures`

- 繼承自 `ControllerBase`

- class 的 summary `A base class for an MVC controller with view support.`
	- 它支援 `View` 相關的東西，又繼承自 `ControllerBase`，所以 `API` 和 `MVC` 都可以繼承它

## 後記

- 會寫這篇的原因是看到官方有些教學是繼承 `ControllerBase`，有些是繼承 `Controller`，覺得很怪才去看原始碼

- 我記得一開始在寫 ASP.NET Core 的時候，都會聽到說和之前的 ASP.NET 不一樣，沒有分 API 和 MVC 了，可以只繼承 `Controller` 就好了，原來它的的原因在此

- 其實如果不知道的話可以都繼承 `Controller` 就好，不過如果比較要求的話，API 應該是繼承 `ControllerBase` 就好了