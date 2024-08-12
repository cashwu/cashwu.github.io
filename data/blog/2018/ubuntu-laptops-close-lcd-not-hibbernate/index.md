---
title: Ubuntu - 筆電關上不休眠
description: 為了省電就把 Ubuntu 灌在筆電上當成 Server，平常都只會用 SSH 連進去操作，也用不到它的螢幕，不過關上筆電時就會休眠，外部無法連線進去，實在是很難搞，搜尋了一下，找到了改設定的方式
date: 2018-12-05 22:30:59.345+08:00
slug: "ubuntu-laptops-close-lcd-not-hibbernate"
tags: [ ubuntu ]
---

為了省電就把 Ubuntu 灌在筆電上當成 Server，平常都只會用 SSH 連進去操作，也用不到它的螢幕，不過關上筆電時就會休眠，外部無法連線進去，實在是很難搞，搜尋了一下，找到了改設定的方式

1、修改 logind.conf

```shell
sudo gedit /etc/systemd/logind.conf
```

2、在檔案裡面找到 `HandleLidSwitch`，取消註解然後把值改成 ignore 存檔

```shell
HandleLidSwitch=ignore
```

3、重啟服務

```shell
 sudo systemctl restart systemd-logind
```


### 參考資料

- [How to Change Lid Close Action in Ubuntu 18.04 LTS](http://tipsonubuntu.com/2018/04/28/change-lid-close-action-ubuntu-18-04-lts/)