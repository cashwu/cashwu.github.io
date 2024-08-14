---
title: Jenkins 換掉內建的 Theme
description: Jenkins 換掉內建的 Theme
date: 2018-12-09 19:40:10.407+08:00
slug: "jenkins-theme"
tags: [ jenkins ]
---

Jenkins 的 Theme 是很單調而且沒有辦法設定，不過有人寫了 Jenkins Theme 的外掛，讓我們可以很容易的換掉原本的 style

1、安裝 [Simple Theme](https://plugins.jenkins.io/simple-theme-plugin) 外掛

2、來這個網站 [jenkins-material-theme](http://afonsof.com/jenkins-material-theme/) 選擇你要的顏色和上傳你的 icon，之後就可以按 `DOWNLOAD YOUR THEME!` 下載一個 css 檔回來

3、到 Jenkins 的設定頁面，找到 Theme 的地方，新增一個 `Extra CSS`，把剛才下載的 css 檔內容貼上

![](/images/404.webp)

4、存檔之後就可以看到不一樣的 Jenkins 了 XD

![](/images/404.webp)