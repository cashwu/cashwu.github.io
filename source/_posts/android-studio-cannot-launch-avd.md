---
title: Android Studio - Cannot launch AVD in emulator
tags:
  - android studio
categories: []
date: 2015-11-07 08:00:00
---

## 問題

安裝完 Android Studio，建立 AVD 後，要開啟時，出現下面的錯誤

![](./android-studio-cannot-launch-avd/01.png)

## 原因

在建立 AVD 的時候，預設是裝在 User 的資料夾下面 (C 槽下面)，而因為我把 User 資料夾搬到 D 槽，所以抓到的路徑為 `D:\Cash\.android\avd`

![](./android-studio-cannot-launch-avd/02.png)

## 解法

加一個 名稱為 `ANDROID_SDK_HOME` 的使用者變數，在安裝 Android Studio 的時候可以指定 SDK 的路徑，這裡的變數值就是當初安裝時指定的路徑

![](./android-studio-cannot-launch-avd/03.png)

![](./android-studio-cannot-launch-avd/04.png)


加完後記得重開 Android Studio，然後建立新的 AVD，AVD 就會被建立在指定的 `ANDROID_SDK_HOME` 路徑下面

![](./android-studio-cannot-launch-avd/05.png)
