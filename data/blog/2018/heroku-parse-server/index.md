---
title: Heroku 無腦架設 Parse Server
description: Parse 是一個 Open Source 的推播服務 Server，很像是 Firebase 的服務，而且可以 Host 在自己的 Server 上面，這裡就用 Heroku 來示範如何無腦的架設 Parse Server
date: 2018-12-22 15:00:46.431+08:00
slug: heroku-parse-server
tags: [ heroku , parse ]
---

[Parse](https://parseplatform.org/) 是一個 Open Source 的推播服務 Server，很像是 `Firebase` 的服務，而且可以 Host 在自己的 Server 上面，這裡就用 Heroku 來示範如何無腦的架設 Parse Server

## Fork Example

- 先把 [parse-server-example](https://github.com/parse-community/parse-server-example)  Fork 到自己的 Github

![](/images/404.webp)

## 在 Heroku 建立一個 APP

![](/images/404.webp)

## 連接到 Github

- 建立完成之後，來到 `Deploy` 的 Tab，中間選擇 `Github`，下面去搜尋剛才 Fork 的 Repository，然後 Connect

![](/images/404.webp)

- Connect 之後來到頁面最下面 `Manual deploy` 的地方，選擇 `Deploy Branch`，手動觸發佈署到 Heroku

![](/images/404.webp)

## 加入 MongoDB

- Parse Server 後面接的是 MongoDB，我們要在 Heroku 多加一個 MongoDB
- 來到 `Resources` Tab，搜尋 `mlab`，選擇`mLab MongoDB`

![](/images/404.webp)

- 方案選擇使用 `Sandbox - Free`

![](/images/404.webp)

## 修改 Parse Server Config

- 來到 `Settings` Tab，點選 `Reveal Config Vars`

![](/images/404.webp)

- 會看到剛才加入的 MongoDB 的連線字串 `MONGODB_URI`，新增兩組 Config Vars
	- APP_ID
	- MASTER_KEY

![](/images/404.webp)

## 瀏覽網頁

- 如果沒有問題的話，瀏覽你的 APP 就會看到測試文字

![](/images/404.webp)

## 測試 Parse

- 可以使用 HTTP 的方式測試 Parse
	- appid 和 host 記得替換成自己設定的

```shell
curl -X POST \
  -H "X-Parse-Application-Id: appid" \
  -H "Content-Type: application/json" \
  -d '{"score":1337,"playerName":"cash","cheatMode":false, "TEST":123 }' \
  http://host/parse/classes/GameScore
```

- 如果成功的話就可以看到返回 objectId 和 createdAt

![](/images/404.webp)