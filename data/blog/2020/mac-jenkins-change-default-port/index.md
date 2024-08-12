---
title: MAC 修改 Jenkins 預設的 Port
description: MAC 修改 Jenkins 預設的 Port
date: 2020-04-26 10:32:45.075+08:00
slug: "mac-jenkins-change-default-port"
tags:  [ jenkins , mac ]
---

- 在之前的文章 ([移除 Jenkins 建立的使用者](https://blog.cashwu.com/mac-remove-jenkins-user)) 裡面有使用一個檔案 `/Library/LaunchDaemons/org.jenkins-ci.plist`，裡面有一個區塊說明真正執行 Jenkins 的 sh 檔位置

![](/images/404.webp)

- 打開 `/Library/Application Support/Jenkins/jenkins-runner.sh` 這個檔案，上面的註解寫了如果你要修改參數的話，檔案位置在 `/Library/Preferrnces/org.jenkis-ci.plist`，然後要使用 `defaults` 這個指令

![](/images/404.webp)

- 修改原本的 port 為 `8082`

> 關於 defaults 可以參考 [wiki](https://en.wikipedia.org/wiki/Defaults_%28software%29) 的說明

```shell
sudo defaults write /Library/Preferences/org.jenkins-ci httpPort 8082
```

- 停止 jenkins 服務在重啟

```shell
sudo launchctl unload /Library/LaunchDaemons/org.jenkins-ci.plist
sudo launchctl load /Library/LaunchDaemons/org.jenkins-ci.plist
```

- 如果重啟後沒有辦法打開網頁的話，可以看一下 log 有什麼錯誤訊息，log 的位置在 `/var/log/jenkins/jenkins.log`