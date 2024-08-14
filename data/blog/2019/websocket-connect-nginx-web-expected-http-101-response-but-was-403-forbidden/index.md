---
title: WebSocket 連接 Nginx 的網站發生 Expected HTTP 101 response but was '403 Forbidden'
description: 使用 WebSocket  去連接 Nginx 使用 Proxy 轉送的網站時發生 Expected HTTP 101 response but was '403 Forbidden'
date: 2019-01-07 12:00:02.984+08:00
slug: 'websocket-connect-nginx-web-expected-http-101-response-but-was-403-forbidden'
tags: [ nginx, websocket ]
---

## 問題

使用 WebSocket 去連接 Nginx 使用 Proxy 轉送的網站時發生 `Expected HTTP 101 response but was '403 Forbidden'`

## 解法

修改 Nginx 的設定檔，Header 的部份要有 `Upgrade` 和 `Connection`，就可以解決了

```shell
server {
	location / {
		proxy_set_header Upgrade $http_upgrade;
		proxy_set_header Connection "upgrade";
	}
}
```