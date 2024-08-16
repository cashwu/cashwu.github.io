---
title: Git 一次刪除所有的 tag
summary: Git 一次刪除所有的 tag
date: 2020-08-27 20:33:43.833+08:00
tags: [ git ]
draft: false
---

很簡單的一行就可以一次刪除所有的 `tag`

```shell
git tag -d $(git tag)
```
