---
title: 'ASP.NET MVC 發佈後找不到 View 問題  02:10'
tags:
  - asp.net mvc
categories: []
date: 2015-08-24 18:39:55
---


## 問題

專案在發佈到 Azure 的 WebSite 後，執行時發生找不到某個 View

## 原因

![](./asp-net-mvc-view-file-not-found/01.png)

在專案的設定檔 (` .csproj` ) 內，找不到的那個 View 為 `None`

## 解法

把 `None` 改為 `Content` 就好了