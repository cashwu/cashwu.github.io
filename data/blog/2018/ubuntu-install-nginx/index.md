---
title: Ubuntu - 安裝 Nginx
description: Ubuntu 安裝 Nginx
date: 2018-12-11 14:10:03.129+08:00
slug: "ubuntu-install-nginx"
tags: [ ubuntu , nginx ]
---

> OS - Ubuntu Desktop 18.04

- 真接用 apt 安裝 nginx 就好

```shell
sudo apt update
sudo apt install nginx
```

- 安裝後可以看一下狀態，應該是 `active`

```shell
sudo systemctl status nginx
```

![](/images/404.webp)

- 如果有啟用 `ufw` 的話，記得先把 80 port 加到 allow 清單

```shell
sudo ufw allow 80
```

- 之後打開 ip 就可以看到 nginx 的畫面了

![](/images/404.webp)

- 預設路徑是放在 `/var/www/` 下面，而 default 的 page 是放在 `/var/www/html` 裡面

![](/images/404.webp)

- 習慣上會把不同的網站放在獨立的資料夾裡面，然後建立獨立的 user 來執行，安全性會比較好

> 後面的文章會把 ASP.NET Core MVC 的專案發佈到 Ubuntu 裡面用 nginx 來作反向代理