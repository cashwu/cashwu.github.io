---
title: Ubuntu - 停用觸控板
description: Ubuntu - 停用觸控板
date: 2012-06-13 16:12:17.092+08:00
slug: "ubuntu-stop-touchpad"
tags: [ ubuntu ]
---

習慣用小紅點之後，常常會不小心碰到觸控板，因為也沒有在用，所以幹脆把它給停用

1. 打開 `始動應用程式`
2. 加入一筆新的，其中 Name 和 Comment 不重要可以隨便打，Command 打上 `sysclient to touchpadoff = 1`
3. 儲存之後重新開機就會生效