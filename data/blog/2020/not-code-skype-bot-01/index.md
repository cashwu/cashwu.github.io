---
title: 不寫一行程式完成簡單的發送訊息 Skype Bot (一)
description: 不寫一行程式完成簡單的發送訊息 Skype Bot
date: 2020-04-25 14:42:14.107+08:00
slug: "not-code-skype-bot-01"
tags: [ azure , bot , skype bot ]
---

> 下一篇文章 [不寫一行程式完成簡單的發送訊息 Skype Bot (二)](https://blog.cashwu.com/blog/not-code-skype-bot-02)

在 Azure 裡面搜尋 `bot` 新增一個 `Bot Channels Registration`

![](./01.webp)

依序輸入相關內容，按下方的`建立`就會產生一個 `Bot`

-   `控制代碼`要全球唯一，所以命名上需要注意
    
-   `訂閱帳戶`就選擇自己的 Azure 帳號
    
-   `資料群組`可以選擇原有的也可以新增新的
    
-   `位置`基本上在台灣的話選擇`東南亞` 會比較快
    
-   `定價`的話選擇 `F0` 就是免費的，相關價錢請參考 [Azure Bot Service pricing](https://azure.microsoft.com/en-us/pricing/details/bot-service/)
    
-   `Application Insights` 如果沒有要用的話就選 `關閉`
    

![](./02.webp)

來到剛才新增的 `Bot`頁面選擇左邊的 `頻道`，原本會有一個 `Web Chat`，點下面的 `Skype` 新增一個

![](./03.webp)

`設定 Skype` 的頁面上面會有一段`警告`可以看一下，如果要把這個 `Bot` 加到群組使用，需要需要修改

![](./04.webp)

切換到 `群組` 下面選擇 `啟用新增至一個群組` ，下面點選 `儲存`，同意 `服務條款`

![](./05.webp)

![](./06.webp)

回到 `頻道` 頁面就可以看到有 `Skype` 在上面，`健康` 的狀態是 `跑步(running)` ，如果沒有用到 `Web Chat` 的話，可以點選後面的 `編輯` 進去刪除

![](./07.webp)

點選 `Skype` ，會出現加入 Skype 聯絡人的頁面，點選 `Add to Contacts`，如果本機有安裝 `Skype` 的話會開啟本機的 `Skype`，然後把 `Bot` 加到你的聯絡人

![](./08.webp)

![](./09.webp)

![](./10.webp)

點選 `設定`，把 `Microsoft App Id` 記起來，這個 `Id` 類似帳號，點選上面的 `管理`，會來到 `憑證及祕密` 頁面

![](./11.webp)

點選 `新增用戶端密碼` ，給定一個 `描述`，設定一個 `到期` 期間，點選 `新增`，會建立一組`密碼`給你，記得存起來，離開這個頁面就看不到了

![](./12.webp)

![](./13.webp)

![](./14.webp)

到這裡 `Skype Bot` 就建立好了，後面會使用另外一個服務叫它發送訊息