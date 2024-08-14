---
title: git include
description: git include
date: 2024-03-31
slug: "git-include"
tags: [ git ]
# tldr: Making GitHub Actions with Js Code
draft: true
---

![](./cover.webp)

`~/.gitconfig`

```gitconfig
[user]
      name = Cash
      email = my@gmail.com
      signingkey = <public key>

[includeIf "gitdir:~/code/"]
    path = ~/code/.gitconfig
```

`~/code/.gitconfig`

```gitconfig
[user]
      name = Cash
      email = company@gmail.com
      signingkey = <public key>
```

```shell
mkdir test && \
cd test && \
git init && \
echo 123 > a.txt && \
git add . && \
git commit -m "test" && \
git log
```

> 圖片來源：網路。若分享內容有侵害您的圖片版權，請來信告知，我們會及時加上版權信息，若是您反對使用，本著對版權人尊重的原則，會儘速移除相關內容。

> Photo by []() on [Unsplash]()


---
{{< ref "/blog/2024/shell-covert-zip-to-7z/index.md" >}}

---

## 問題
## 原因
## 解法

## 參考連結