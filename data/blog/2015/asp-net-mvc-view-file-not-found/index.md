---
title: ASP.NET MVC - 發佈後找不到 View 問題
description: ASP.NET MVC 發佈後找不到 View 問題
date: 2015-08-24 20:47:36.281+08:00
slug: "asp-net-mvc-view-file-not-found"
tags: [ asp.net mvc ]
---

## 問題

專案在發佈到 Azure 的 WebSite 後，執行時發生找不到某個 View

## 原因

- 在專案的設定檔 (`.csproj` ) 內，找不到的那個 View 為 `None`

![](/images/404.webp)

## 解法

在專案檔裡面把 `None` 改為 `Content` 就好了