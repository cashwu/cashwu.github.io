---
title: MongoDB - (二) 安裝成服務
description: 安裝 MongoDB 變成 Windows Service
date: 2018-04-07 05:20:35.818+08:00
slug: "mongodb-02-install-system-service"
tags: [  mongodb ]
---

> OS : Windows 10 pro 64bit

- 使用 administrator 啟動 `cmd`，輸入 `mongod --config "C:\MongoDB\mongod.cfg" -install`

![](/images/404.webp)

- 在服務裡面就可以看到 mongodb 

![](/images/404.webp)

- 使用 cmd 啟動服務 `net start mongodb`

![](/images/404.webp)

- mongodb 服務的狀態就會變成 `執行中`

![](/images/404.webp)