---
title: ASP.NET Core 實作雙重驗證 (2FA)
description: 你的網站有雙重驗證 (Two-factor authentication，通稱 2FA) 嗎？來看一下怎麼使用  ASP.NET Core 實作 2FA 幫網站增加安全性吧 !!
date: 2019-01-08 14:35:14.445+08:00
slug: "asp-net-core-two-factor-authenticator"
tags: [ asp.net core ]
---

你的網站有雙重驗證 (`Two-factor authentication`，通稱 `2FA`) 的功能嗎 ? 來看一下怎麼使用  ASP.NET Core 實作 2FA 幫網站增加安全性吧 !!

> ASP.NET Core 2.2

## 安裝套件

- [GoogleAuthenticatorService.Core](https://www.nuget.org/packages/GoogleAuthenticatorService.Core)

## 產生 QRCode

- 先初始化剛才安裝的套件
	- 第一個參數為 `Title`
	- 第二個參數為 `User 代碼`，這裡用的是我的 Email
	- 第三個參數為 `SecreKey`，這裡很簡單的只使用 Key，真實的環境請自行設置夠安全的 SecreKey
	- 第四和第五個參數為 `QRCode` 的寬和高

```csharp
var Authenticator = new TwoFactorAuthenticator();
var setupInfo = Authenticator.GenerateSetupCode("Cash Google Auth",
                                                "cash@cashwu.com",
                                                "key",
                                                250,
                                                250);
```

- 初始化之後就可以用它的 Property 拿到相關的資訊
	- `QrCodeSetupImageUrl` 為 QRCode 的網址，這裡會使用 [`Google Charts`](https://developers.google.com/chart) 的 API 產生 QRCode
	- `ManualEntryKey` 為手動輸入的密鑰

```csharp
var qrCodeUrl = setupInfo.QrCodeSetupImageUrl;
var manualCode = setupInfo.ManualEntryKey;
```

- 放在網頁上測試
	- 可以看到 QRCode 和 Manual Key

![](/images/404.webp)

## 使用 Google Authenticator APP 測試

- 使用 APP 掃 QRCode
	- 可以看到上面有我們設定的 Title 和 Email

![](/images/404.webp)

- 使用 Manual Key 手動輸入

![](/images/404.webp)

- 可以看到下面多了一個手動輸入的 2FA，產生的號碼是一樣的，只是它沒有 Title 而已

![](/images/404.webp)

## 驗證

- 使用 `ValidateTwoFactorPIN` 方法，就可以驗證 2FA 是不是 Valid
	- 第一個參數為產生 QRCode 使用的 `SecreKey`
	- 第二個參數為要驗證的`數字`

```csharp
var Authenticator = new TwoFactorAuthenticator();
var valid = Authenticator.ValidateTwoFactorPIN("key", code);
```

- 測試 APP 產出的數字是不是可用的

![](/images/404.webp)

## 後記

- 使用套件就可以產生 2FA 實在是很方便，可以幫自己的網站增加不少安全性
- 有時間的話應該把前端的程式碼也包成套件，會比較方便使用
- 使用這個套件還沒有辦法作到像其它平台一樣有 Recovery Code 的功能，可能需要自己實作了