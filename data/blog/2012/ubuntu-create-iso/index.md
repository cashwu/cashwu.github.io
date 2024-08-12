---
title: Ubuntu - 建立光碟 ISO 檔
description: Ubuntu - 建立光碟 ISO 檔
date: 2012-06-05 16:11:21.194+08:00
slug: "ubuntu-create-iso"
tags: [ ubuntu ]
---

`Command > df` ( 查看磁碟分割區 )，如果是光碟機的話 應該會是 /dev/sr0

`Command > cat /dev/sr0 > myiso.iso` ( df 出來的光碟機掛載名稱 > 檔案名)

這個時候 `myiso.iso` 檔案就會存在 `家目錄` 下