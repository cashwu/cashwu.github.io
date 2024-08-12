---
title: Ubuntu - 查詢 IP
description: Ubuntu 查詢 IP
date: 2018-12-08 19:11:41.311+08:00
slug: "ubuntu-ifconfig-ip"
tags: [ ubuntu ]
---

> OS - Ubuntu Desktop 18.04

1、查詢 ip 在 windows 是 `ipconfig` 在 ubuntu 是 `ifconfig`，如果你打 `ipconfig` 時還會提醒你是不是打錯了

![](/images/404.webp)

2、預設 ubuntu 是沒有安裝這個套件的，你打 `ifconfig` 會提醒你要安裝 net-tools

```shell
sudo apt install net-tools
```

![](/images/404.webp)

3、安裝好了再打 `ifconfig` 就可以得到 ip 的相關資訊

![](/images/404.webp)