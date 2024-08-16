---
title: MAC 移除 Jenkins 建立的使用者
summary: 在 MAC 安裝 Jenkins 時，會建立一個使用者來運行 Jenkins，如果只是在自己的本機運行，沒有安全性的疑慮，是可以把這個使用者移除的。
date: 2019-04-19 10:30:21.295+08:00
tags: [ jenkins , mac ]
draft: false
---

接續上一篇 [MAC 安裝 Jenkins](https://blog.cashwu.com/mac-install-jenkins)，在 MAC 安裝 Jenkins 時，會順便建立一個使用者來運行 Jenkins，如果只是在自己的本機運行，沒有安全性的疑慮，是可以把這個使用者移除的，不然每次登入就要先選擇使用者，其實有點麻煩，下面就來看如何移除這個使用者吧 !

- 停止 Jenkins

```shell
sudo launchctl unload /Library/LaunchDaemons/org.jenkins-ci.plist
```

- 修改執行 Jenkins 的使用者和群組
	- 編輯 `org.jenkins-ci.plist`，如果不會用 vim，也可以用自己習慣的編輯器
		- GroupName 下面替換成 `staff` (參考圖片)
		- UserName 下面替換成自己登入電腦的帳號 (參考圖片)

```shell
sudo vim /Library/LaunchDaemons/org.jenkins-ci.plist
```

![](/static/images/404.webp)

- 修改相關資料夾的權限
	- 把下面的 <帳號> 替換成自己登入電腦的帳號

```shell
sudo chown -R <帳號>:staff /Users/Shared/Jenkins/
sudo chown -R <帳號>:staff /var/log/jenkins/
```

- 重啟 Jenkins

```shell
sudo launchctl load /Library/LaunchDaemons/org.jenkins-ci.plist
```

- 刪除電腦的使用者
	- 在 `系統偏好設定 -> 使用者與群組`裡面應該會看到一個沒有名稱的使用者
	- 按下面的 `-` 就可以刪除使用者了

![](/static/images/404.webp)