---
title: 容昜的找到 Skype 的 群組 (Group) Id
description: 容昜的找到 Skype 的 群組 (Group) Id
date: 2020-04-25 15:32:02.554+08:00
slug: "easy-find-skype-group-chat-id"
tags: [ skype bot ]
---

打開 `Skype` 的[網頁版](https://web.skype.com/)，點到你要找的群組

![](./01.webp)

打開`開發者工具` 的 `網路` ，先 `清除` 原有的 log

![](./02.webp)

在`群組` 裡面隨打一個訊息，就會看到網路會有一個 `messages` 的訊息送出，在右邊的視窗面看到送出的 `Url` ，把 `conversations` 後面的 `//` 裡面的文字 copy 出來

![](./03.webp)

來到 [URL Decoder/Encoder](https://meyerweb.com/eric/tools/dencoder/) 頁面，把上面的文字貼入，點選 `Decode`，原本的文字就會被 `Decode` 之後的文字取代掉

![](./04.webp)

![](./05.webp)

Group Id 就是這串文字，`19:` 開頭，`@thread.skype` 結尾

> `19:XXXXXXXXX@thread.skype`