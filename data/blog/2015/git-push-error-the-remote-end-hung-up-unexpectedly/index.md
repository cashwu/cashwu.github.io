---
title: Git - Push Error The remote end hung up unexpectedly
description: Git Push Error The remote end hung up unexpectedly
date: 2015-06-30 21:52:13.896+08:00
slug: "git-push-error-the-remote-end-hung-up-unexpectedly"
tags: [ git ]
---

## 問題

今天在 `git push` 時發生了錯誤

```shell
Unable to rewind rpc post data - try increasing http.postBuffer 
error: RPC failed; result=56, HTTP code = 0 
fatal: The remote end hung up unexpectedly
```

## 原因

上傳的檔案過大造成錯誤

## 解法

加大 Git 的 postBuffer，後面的數字是自己決定的大小，以下面來看是 50M

```shell
git config --global http.postBuffer 524288000
```

### 參考連結

- [HTTP 狀態碼](https://zh.wikipedia.org/wiki/HTTP%E7%8A%B6%E6%80%81%E7%A0%81)
- [Git 儲存庫太大導致無法上傳 Visual Studio Online 如何處理](http://blog.miniasp.com/post/2014/09/07/Handle-large-Git-repository-on-Visual-Studio-Online.aspx)