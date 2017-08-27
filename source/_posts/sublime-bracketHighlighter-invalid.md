---
title: Sublime BracketHighlighter 失效問題
tags:
  - sublime
categories: []
date: 2013-07-15 08:00:00
---

在 Sublime Text 裡面有一個很有名的高亮套件 [BracketHighlighter](https://github.com/facelessuser/BracketHighlighter/)，
自己在顯示上跟看到別人的長的不太一樣，後來發現只是設定的問題

請參考下圖進入 BracketHighlighter 的設定檔

![](./Sublime-BracketHighlighter-Invalid/01.png)

打開設定檔後，按 `Ctrl + F`，搜尋 `bracket_styles`，會看到它的下面有一個 `default` 的設定區塊

- color 為 `brackethighlighter.default`，style 為 `underline`，可以看到 { } 的下方有一條白色的高亮 ( 這是預設的設定 )

![](./Sublime-BracketHighlighter-Invalid/02.png)

- color 為 `entity.name.class`，style 為 `underline`，可以看到 { } 下方的白色變成 綠色了 ( 不確定這個顏色是不是跟用的 Theme 有關 )

![](./Sublime-BracketHighlighter-Invalid/03.png)

- color 為 `brackethighlighter.default`，style 為 `hightlight` 可以看到 { } 的高亮長高了

![](./Sublime-BracketHighlighter-Invalid/04.png)

- 後來發現 設定成 solid 跟 hightlight 的效果一樣

![](./Sublime-BracketHighlighter-Invalid/05.png)
![](./Sublime-BracketHighlighter-Invalid/06.png)

- 設定成 outline 的樣子

![](./Sublime-BracketHighlighter-Invalid/07.png)
