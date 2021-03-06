---
title: ASP.NET MVC Controller (一)
tags:
  - mvc
  - controller
categories: []
date: 2014-07-15 08:00:00
---

## Controller 的基本條件

![](./aspnet-mvc-controller-01/01.png)

1. Controller 要 `public class`
2. Controller name 要以 ``Controller 結尾`
3. 需繼承 `ASP.NET MVC 內建的 Controller 類別` 或 繼承 '有實作 IController` 的 class 或 `自已實作 IController`

## Action 的基本條件

- Action 要 `public class`，任何 `非公開方法` 都不會被視為一個動作方法

## BaseController

可以在 `Controller` 裡面寫一個 `BaseController`，
把需要共用的程式寫在這裡，在讓所有的 Controller 繼承 `BaseController`

例如：我們可以在 `BaseController` 裡面，override `HandleUnknownAction` 自已去處理 `404` 的狀況，
如果找不到頁面的話就導向到 `/Home/Index`

![](./aspnet-mvc-controller-01/02.png)

不過這樣子寫會有一些問題，如果是 `Ajax` 的時候，會返回一整個導向的頁面，
所以需要利用 `Request.IsAjaxRequest()` 作判斷，並使用原本 `base 的方法`

![](./aspnet-mvc-controller-01/03.png)