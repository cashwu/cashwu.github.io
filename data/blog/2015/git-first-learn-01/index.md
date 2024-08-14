---
title: Git - 第一次學 Git 就上手 - 01 建立第一個 Git 版控
description: Git 第一次學 Git 就上手 01 建立第一個 Git 版控
date: 2015-02-08 08:22:12.349+08:00
slug: "git-first-learn-01"
tags: [ git ]
---

> - 使用 os 為 windows
> - 使用軟體為 [TortoiseGit](https://code.google.com/p/tortoisegit/)
> - 文章大部份內容來自於 [保哥的 Git 版本控管實戰：新手入門篇](http://miniasp.kktix.cc/) 上課內容

#### 建立一個本地儲存庫

在想要作版控的資料夾裡面 按右鍵選 `Git Create repository here`

![](/images/404.webp)

會跳出一個訊問  `Make it Bare` 的視窗，不要勾選 `Make it Bare`，按 `OK`

![](/images/404.webp)

建立完成後，會跳出訊息跟你說已經建立一個空的 Git 儲存庫，而且資料夾會出現一個 `.git` 的隱藏資料夾

![](/images/404.webp)

在資料夾裡面新增一個文字檔 (內容不重要，也可以是任意的檔案)

![](/images/404.webp)

#### 把檔案加入版控

在資料夾裡面按右鍵選擇 `Git Commit -> master`
(表示要 Commit 到 master 這個分支，後面會說明分支的部份，目前可以先不理它，只要先知道 Commit 就可以了)

![](/images/404.webp)

這個時候會看到剛才新增的檔案為 `Unknown` 的狀態

![](/images/404.webp)

要先把檔案加入版控，可以針對單一檔案按右鍵選擇 `Add` 加入

![](/images/404.webp)

如果有兩個以上的檔案要加入時，可以按 `Ctrl + A` (全選)，或是用滑鼠選取檔案

![](/images/404.webp)

之後在任一檔案上按右鍵選擇 `Add`，就可以加入所選取的檔案

![](/images/404.webp)

完成後會出現成功的訊息，跟你說加入了那個檔案是成功還是失敗，點選 `ok` 關掉視窗

![](/images/404.webp)

再回來看檔案的狀態，可以看到己經變為 `Added` 已加入的狀態

![](/images/404.webp)

在上方 `Message` 的地方打上你所要註記的訊息後，按下 `ok`

![](/images/404.webp)

會跳出一個執行視窗，裡面看到 `Success` 就表示已經完成簽入的動作，按 `Close` 關掉

![](/images/404.webp)

回到原本作版控的資料夾，看到檔案前面有多出一個綠色的勾勾就表示該檔案已經被版控了

![](/images/404.webp)