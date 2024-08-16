---
title: Ubuntu - SSH 安全性設定
summary: Ubuntu SSH 安全性設定
date: 2018-12-10 11:04:26.753+08:00
tags: [ ubuntu ]
draft: false
---

> OS - Ubuntu Desktop 18.04

[上一篇文章]({{< ref "/blog/old/2018/ubuntu-ssh-remote-connection/index.md" >}}) 我們已經用了 SSH 登入到遠端的 Server，我們可以修改預設的 SSH 設定讓他變的比較安全

1、SSH 的 config 在 `/etc/ssh/sshd_config` 裡面

```shell
sudo vim /etc/ssh/sshd_config
```

2、禁止 Root 登入，取消註解 `PermitRootLogin` 並設定成 `no`

```shell
PermitRootLogin no
```

3、禁止打帳號密碼登入，取消註解 `PasswordAuthentication` 並設定成 `no`

```shell
PasswordAuthentication no
```

4、使用憑證登入，取消註解 `PubkeyAuthentication`，基本上不設定預設為 `yes`

```shell
PubkeyAuthentication yes
```

5、設定可 SSH 登入的使用者，在最下面新增 `AllowUsers`，設定使用者名稱，多個時用空白分隔

```shell
AllowUsers cash www
```

6、修改後存檔，重啟 SSH 服務

```shell
sudo systemctl restart sshd
```