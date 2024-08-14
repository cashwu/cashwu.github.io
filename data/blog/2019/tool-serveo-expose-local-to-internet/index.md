---
title: 內網穿透神器 Serveo 介紹 
description: 內網穿透神器 Serveo 介紹
date: 2019-04-27 15:19:49.26+08:00
slug: "tool-serveo-expose-local-to-internet"
tags: [ tool ]
---

如何在 local 測試的時候把測試的網站讓外部可以透過網路連結，使用 `Serveo` 是非常方便的工具，在官網裡面有寫到，不需要安裝和註冊即可使用，和另一個神器 `Ngrok` 相比，如果兩個都以免費的角度來看的話，`Serveo` 實在是強大許多，下面就來看如何使用 `Serveo` 吧 !!

> Serveo [官網](https://serveo.net/)

## 基本使用

- 如果要把本機的 Jenkins 給對外時可以使用下面的指令，然後上面就會給你一個可以使用的網址

```shell
ssh -R 80:localhost:8080 serveo.net
```

![](/images/404.webp)

- 打開網頁測試，這個網址真的可以連到，而在 cmd 也會顯示從那一個 ip 連接的

![](/images/404.webp)

![](/images/404.webp)

## 自定 Subdomain

- 如果要自定義前面的 Subdomain 的話可以在前面在多加上 Subdomain 的名稱

```shell
ssh -R cashwuci:80:localhost:8080 serveo.net
```

![](/images/404.webp)

- 測試

![](/images/404.webp)

![](/images/404.webp)

- 名稱重復的話會出錯，不過它不會跟你說是名稱重復，只會跟你說 forwarding 失敗

![](/images/404.webp)

## Forward 網址

- 它當然也可以 Forwarding 不在本機的一個網址，下面以自己的 Blog 為例

![](/images/404.webp)

- 測試

![](/images/404.webp)

![](/images/404.webp)

## GUI session

- 在啟動時會有一個提示，按 `g` 可以啟動 `GUI session`

![](/images/404.webp)

- 按 `g` 之後會切頁，然後會顯示相關的操作

![](/images/404.webp)

- 當有 Request 時會呈現每一個 Request 的連接時間

![](/images/404.webp)

- 如果按上下選擇的話，下面會出現 Request 的內容

![](/images/404.webp)

## 後記

`Serveo` 真的是很強大的工具，而且免費就可以自定 Subdomain，其實它也可以自定 Domain，只是我沒有測試，然後也可以自己 Host 在自己的機器上面，只是免費的限制只可以使用三個通道而已