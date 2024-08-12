---
title: ASP.NET Core 自定專案範本
description: 每次在建立 ASP.NET Core 新專案時，如果分層分的比較細，需要加入很多專案，而且每個專案都要安裝很多套件，實在是很花時間。如果可以建立自己的專案範本，就跟內建的範本一樣，應該可以節省不少的時間，在公司裡面也可以變成一個專案的標準範本，我們就來看如何在 ASP.NET Core 建立自定專案範本吧 !!
date: 2019-01-03 10:00:51.135+08:00
slug: "asp-net-core-custom-project-templates"
tags: [ asp.net core ]
---

每次在建立 ASP.NET Core 新專案時，如果分層分的比較細，需要加入很多專案，而且每個專案都要安裝很多套件，實在是很花時間。如果可以建立自己的專案範本，就跟內建的範本一樣，應該可以節省不少的時間，在公司裡面也可以變成一個專案的標準範本，我們就來看如何在 ASP.NET Core 建立自定專案範本吧 !!

> ASP.NET Core 2.2
> macOS

## 新增專案

- 新增一個 Web 專案和一個測試專案，記得要有 Solution

> 名稱非常重要，這裡使用 `Tmpl`，比較不會被程式使用到，因為變成範本之後，這個名稱會被替換掉，所以如果取的不好的話，會不小心被替換掉，必須要非常的小心

![](/images/404.webp)

- 在原本的 Solution 資料夾裡面多一個 `Content` 資料夾，然後把所有的東西移到這個資料夾裡面

![](/images/404.webp)

## 建立 Template Config

- 在 `Content` 資料夾裡面建立一個 `.template.config` 資料夾，然後在這個資料夾裡面建立一個 `template.json` 檔案

![](/images/404.webp)

- template.json 內容如下
	- 裡面比較重要的地方應該是 `sourceName`，就是前面有提到的，之後如果要新增專案的話，新專案名稱會把 `sourceName` 設定的字串給替換掉
	- `identity` 只是一個唯一的示別名稱，跟 `shortName` 一樣就好
	- `tags` 的 `type` 設定成 `project`
	- `preferNameDirectory` 一般都為 `true`，指的是如果建立專案時未使用 `-n` 指定專案名稱時，使用資料名稱作為專案名稱
	- 其它的設定請參考 template.json 和專案範本的關係圖

![](/images/404.webp)

![](/images/404.webp)

## 新增資料夾範本

- 使用 `dotnet new -i 資料夾路徑` 來新增資料夾的專案範本，新增之後就可以看到自己的範本在上面了
	- 資料夾為指定到 `Content` 資料夾的上一層路徑，而且必須要使用 `完整路徑` 來註冊

![](/images/404.webp)

- 新增專案測試一下 `dotnet new cashmvc -o CashTmpl`

![](/images/404.webp)

- 可以看到兩個專案就直接建立好了，名稱已經是我們給的 `CashTmpl`

![](/images/404.webp)

- 移除資料夾的專案範本，把原本新增的指令 `-i` 改成 `-u`，就可以看到範本已經被移除了

![](/images/404.webp)

## Nuget 設定

- 在和 `Content` 同一層的地方，新增一個 `Tmpl.nuspec` 的 nuget 設定檔

![](/images/404.webp)

- 內容如下
	 - 重點在於 `file` 的設定，`src` 指的是什麼東西要被打包成 `nuget package`，`exclude` 指的是什麼東西要被排除，這裡設定的是 `.idea` Rider 的設定檔和 MAC 的 `.DS_Store` 檔案，多個設定時使用 `,` 分隔
	 - 其它的設定請參考[官方說明 - 建立 NuGet 套件](https://docs.microsoft.com/zh-tw/nuget/create-packages/creating-a-package)

![](/images/404.webp)

- 使用 `nuget pack nuspec檔` 打包成 package
	- 會產生一個 `xxx.nupkg` 的 package 檔案

![](/images/404.webp)

## 新增 Nuget 範本

- 指令跟使用資料夾差不多，變成指定 package 的名稱，而因為這個 package 範本沒有推上 nuget server，所以直接指定檔案就好了

![](/images/404.webp)

- 如果要移除時，記得指定的是 package 的名稱

![](/images/404.webp)

## 後記

- ASP.NET Core 在設定專案範本上實在是簡單許多，一些小地方注意一下就好了
- 建立完範本實在是幫之後新增專案省了不少的時間，尤其是專案個數多達 7 個時，每個都要設定很麻煩，而且又有預設要有的程式碼和套件
- 如果把 package 推上自家的 nuget server，在公司裡面就可以變成大家之後新增專案的固定範本，即可以省下時間，又可以變成公司的規範，好處多多