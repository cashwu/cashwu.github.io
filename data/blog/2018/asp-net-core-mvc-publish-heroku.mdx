---
title: ASP.NET Core MVC + Heroku
summary: 把 ASP.NET Core MVC 專案發佈到 Heroku 平台上
date: 2018-12-12 21:32:14.151+08:00
tags: [ asp.net core , heroku ]
draft: false
---

把 ASP.NET Core MVC 專案發佈到 Heroku 平台上

> ASP.NET Core MVC 2.2

- 登入 Heroku 平台建立一個 APP

![](/static/images/404.webp)

- 建立完 APP 之後在 Deploy 的地方有教你怎麼用 Heroku CLI 把程式碼傳到 Heroku 的 Git，下面就按照步驟來作吧

![](/static/images/404.webp)

- 建立一個 ASP.NET Core MVC 專案並且確定可以建置執行

```shell
dotnet new mvc -o cashwumvc
dotnet build
```

- 把專案加到 Git

```shell
git init
git add .
git commit -m "init"
```

- 登入 Heroku CLI

```shell
heroku login
```

![](/static/images/404.webp)

- 設定 Git Remote 為 Heroku

```shell
heroku git:remote -a cashwumvc
```

![](/static/images/404.webp)

- 加入 Heroku Build 的外掛套件 [dotnetcore-buildpack](https://github.com/jincod/dotnetcore-buildpack)，才可以把程式碼 push 到 Heroku 的時候 Build 成 Heroku 可以執行的 APP

```shell
heroku buildpacks:set https://github.com/jincod/dotnetcore-buildpack
```

![](/static/images/404.webp)

- 把程式碼 push 到 Heroku，從 console 就可以看到 remote 一直在跑，先安裝 SDK、Runtime 然後是安裝套件，最後是 Build 以及發佈

```shell
git push heroku master
```

![](/static/images/404.webp)

- 最後可以打開 APP 的網址 `https://cashwumvc.herokuapp.com/`，就可以看到網站了

![](/static/images/404.webp)

> 不得不說自從 .NET Core 可以跨平台之後，就不一定跑在 Windows (Azure) 上面了，而且想不到連 Heroku 也有支援 .NET Core，如果有免費網站的需求，又多了一個選擇，不過記得要看一下免費的[限制條件](https://www.heroku.com/pricing)，如果有付費的需求，最低 7 鎂/月，就可以有 SSL + Customer Domain + Application Metrics，跟 Azure 比起來實在是太便宜了 XDD