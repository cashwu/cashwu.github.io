---
title: Ubuntu 建立光碟 ISO 檔
tags:
  - ubunut
categories: []
date: 2012-06-05 08:00:00
modified: 2012-06-05 08:00:00
---

`Command > df` ( 查看磁碟分割區 )，如果是光碟機的話 應該會是 /dev/sr0

`Command > cat /dev/sr0 > myiso.iso` ( df 出來的光碟機掛載名稱 > 檔案名)

這個時候 `myiso.iso` 檔案就會存在 `家目錄` 下