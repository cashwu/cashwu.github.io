---
title: 不寫一行程式完成簡單的發送訊息 Skype Bot (二)
summary: 不寫一行程式完成簡單的發送訊息 Skype Bot
date: 2020-04-25 17:44:55.774+08:00
tags: [ bot , integromat , skype bot ]
draft: false
---

> 上一篇文章 [不寫一行程式完成簡單的發送訊息 Skype Bot (一)](https://blog.cashwu.com/blog/not-code-skype-bot-01)

這裡會使用 `integromat` 這個服務來整合 `Skype Bot`，先到 [https://www.integromat.com/](https://www.integromat.com/) 註冊一個帳號，相關的價錢請參考 [pricing 頁面](https://www.integromat.com/en/pricing)

登入到 `Dashboard` 頁面後，點選左邊的 `Scenarios`，然後點選右上角的 `Create a new scenario`，新增一個情境

![](./01.webp)

![](./02.webp)

因為我們後面會使用 `api` 的方式叫 `Bot` 送訊息，所以這裡可以先搜尋 `webhooks` ，選擇 `Webhooks` 然後點選 `Continue`

![](./03.webp)

來到 `Scenario` 的編輯畫面，點選中間園圈的 `?` 選擇 `Webhooks`

![](./04.webp)

![](./05.webp)

選擇 `Custom Webhook`

![](./06.webp)

點選 `Add` 新增一個新的 `hook`

![](./07.webp)

給 `hook` 一個名稱，`IP restrictions` 因為是測試所以就不給，建議實務上使用會比較安全，點選 `Save`

![](./08.webp)

畫面上出現的 `Url` 就是要使用的 `api` ，下面會有一個一直在轉的符號，等待解析收到的資料，複製 `Url`

![](./09.webp)

這裡打開你的 `http` 工具，我在 `Mac` 上面使用的是 `Paw`，使用 `Post` 送出一段 `json` ，你會的到 `Accepted 200`

![](./10.webp)

畫面上會出現 `Successfuly determined.` 代表已經解析好收到的資料了，點選 `OK` 儲存

![](./11.webp)

移到 `Webhooks` 右邊的小圓圈，點選 `Add another module`，搜尋 `skype` ，點選 `Skype`

![](./12.webp)

![](./13.webp)

![](./14.webp)

然後點選 `Send a message`

![](./15.webp)

出現 `skype` 的設定畫面，點 `Add` 新增一個新的設定

![](./16.webp)

給定一個`名稱`，這裡的 `Microsoft App Id` 和 `Password` (請參考上一篇文章 [不寫一行程式完成簡單的發送訊息 Skype Bot (一)](https://blog.cashwu.com/blog/not-code-skype-bot-01) )，點選 `Continue` 之後會跳出一個新的頁面確定連線是否正常，好了之後可以看到 `Connection` 有我們剛才新增的名稱

![](./17.webp)

![](./18.webp)

`Conversation Id` 裡面填入 Skype Group Id (請參考 [容昜的找到 Skype 的 群組 (Group) Id](https://blog.cashwu.com/blog/easy-find-skype-group-chat-id))，點選下方的 `Activiy - Text` 會跳出視窗，裡面會有一開始解析到的資料的`名稱`，把它 `拖` 進去，按下 `OK` 就建立好了

![](./19.webp)

![](./20.webp)

回到畫面可以看到 `Webhooks` 已經串接到 `Skype`，記得點選最下方的 `Save` 儲存所有的設定

![](./21.web)

回到 `Scenario` 的畫面點選剛才新增的那一筆，把開關打開

![](./22.webp)

![](./23.webp)

使用 `http` 工具再發送一次，就可以看到 `skype` 收到訊息了

![](./24.webp)