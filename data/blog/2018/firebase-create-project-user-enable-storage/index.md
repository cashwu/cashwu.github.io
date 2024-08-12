---
title: 如何在 Firebase 建立專案、建立使用者和啟用 Storage
description: Firebase 是 Google 的一個服務，提供開發者可以在雲端快速建置後端的相關服務，例如登入、資料庫和儲存空間等，而且每一項服務都有免費的額度可以讓我們使用，真的是很方便，首先就來看如何在 Firebase 建立專案、建立使用者和啟用 Storage
date: 2018-12-27 21:46:19.942+08:00
slug: "firebase-create-project-user-enable-storage"
tags: [  firebase ]
---

Firebase 是 Google 的一個服務，提供開發者可以在雲端快速建置後端的相關服務，例如登入、資料庫和儲存空間等，而且每一項服務都有免費的額度可以讓我們使用，真的是很方便，首先就來看如何在 Firebase 建立專案、建立使用者和啟用 Storage

## 建立專案

- 登入 Firebase 之後來到首頁，點 `新增專案`

![](/images/404.webp)

- 給專案一個名稱，專案 ID 基本上會跟專案名稱一樣，如果系統覺得你的專案名稱不符合會幫你加後綴

![](/images/404.webp)

- 這頁基本上都可以不用選，直接 `建立專案`

![](/images/404.webp)

- 等它轉完就建立好了

![](/images/404.webp)

## 新增使用者登入

- 建立完成來到專案首頁點左邊的 `Authentication`

![](/images/404.webp)

- 先設定一個登入方式

![](/images/404.webp)

- 點選第一個`電子郵件/密碼`

![](/images/404.webp)

- 啟用後儲存

![](/images/404.webp)

- 回來就可以看到已經啟用了

![](/images/404.webp)

- 點回 `使用者`，點選 `新增使用者`

![](/images/404.webp)

- 輸入 Email 和 密碼，新增使用者

![](/images/404.webp)

- 回來就可以看到有一個使用者

![](/images/404.webp)

## Storge

- 點左邊的 `Storage`，點選 `開始使用`

![](/images/404.webp)

- 一開始會提醒你預設的安全性規格

> 允許所有人讀取，要有權限才可以寫入

![](/images/404.webp)

- 之後可以來到 `規則` 修改安全性規格

![](/images/404.webp)

- 點回到 `檔案`，會看到中間有 Storage 的 `URL`

![](/images/404.webp)

> 如果要手動上傳檔案，可以點選右上角的 `上傳檔案`

## API Key

- 點上面的`齒輪`，點`專案設定`

![](/images/404.webp)

- 就可以看到 API Key

![](/images/404.webp)

## 後記

- 之後會使用 ASP.NET Core 上傳檔案到 Firebase 的 Storage
	- 會使用到使用者的 `帳號`、`密碼`、`Storage URL` 和 `API Key`