---
title: Git 一次刪除所有的 tag
description: Git 一次刪除所有的 tag
date: 2020-08-27 20:33:43.833+08:00
slug: "git-delete-all-tag"
tags:  [ git ]
---

很簡單的一行就可以一次刪除所有的 `tag`

```shell
git tag -d $(git tag)
```
