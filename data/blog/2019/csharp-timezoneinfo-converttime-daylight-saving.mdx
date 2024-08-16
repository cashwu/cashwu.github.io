---
title: C# 使用 TimeZoneInfo 轉換時區遇到 Daylight Saving 的問題
summary: C# 使用 TimeZoneInfo 轉換時區遇到 Daylight Saving 的問題
date: 2019-04-15 19:09:10.794+08:00
tags: [ c# , convert , datetime ]
draft: false
---

今天看到主廚大大寫了一篇文章 [「桌邊服務」DateTime 本身有沒有包含時區的資訊？](https://dotblogs.com.tw/supershowwei/2019/04/15/095324)，提到時區和轉換的問題，想到之前解決的一個 Bug 就提醒了一下遇到 Daylight Saving 時可能會發生問題，順手寫了這篇文章

## 問題

程式碼如下，把一個時間的時區從中歐的標準時間轉換成 Local 的時間

```csharp
var dt = new DateTime(2019, 3, 31, 2, 28, 0);
var estTimeZone = TimeZoneInfo.FindSystemTimeZoneById("Central Europe Standard Time");
var estdt = TimeZoneInfo.ConvertTime(dt, estTimeZone, TimeZoneInfo.Local);
```

執行之後應該會得到 exception，簡單的來說就是這個時間有問題，無法轉換

> System.ArgumentException: The supplied DateTime represents an invalid time.  For example, when the clock is adjusted forward, any time in the period that is skipped is invalid.
Parameter name: dateTime

## 原因

這個要轉換的時間，對於中歐的標準時間來說剛好是 2019 Daylight Saving 要開始的第一個小時，因為之後會變快一個時間，所以第一個小時是有問題的

> 可以在[這裡](https://time.artjoey.com/)查詢 Daylight Saving 的時間

## 解法

最簡單的解法是轉換前先判斷是不是 `InvalidTime`，然後跳過這一個小時

```csharp
var dt = new DateTime(2019, 3, 31, 2, 28, 0);
var estTimeZone = TimeZoneInfo.FindSystemTimeZoneById("Central Europe Standard Time");
if (estTimeZone.IsInvalidTime(dt))
{
	dt = dt.AddHours(1);
}
var estdt = TimeZoneInfo.ConvertTime(dt, estTimeZone, TimeZoneInfo.Local);
```

## 後記

基本上如果不是之前有遇到剛好在這一個小時的時區轉換問題，也不會知道，真是可遇不可求的 Bug