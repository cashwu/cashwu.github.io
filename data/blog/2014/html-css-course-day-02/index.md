---
title: Course - 網頁實戰入門 (HTML x CSS) Class Day 02
description: 網頁實戰入門 (HTML x CSS) Class Day 02
date: 2014-08-31 10:26:15.37+08:00
slug: "html-css-course-day-02"
tags:  [ course ]
---

## 會影響 layout 排版
 1. display
 2. position
 3. float
 4. margin
 5. padding
 6. width/height

## max-width 最大寬度
 - 視窗放大縮小時，會跟著視窗跑，可以運用在 RWD
 - 固定寬度的話，視窗放大時會被固定，縮小時會出現橫向捲軸
 - 圖片的話可以給 max-width = 100%，就可以跟著視窗放大縮小

## Box Model
 - 使用 margin 不會改變原本 div 的寬度
 - div 裡面的資料作縮排的話用 padding，如果是 div 跟 div 之間的排版的話用 margin
 - border 算是 div 的寬度，所以排版的話還是會從左邊開始排版
 - 如果要了解 div 的大小的話，一般會設定 background 用來測試看看是那裡跑版
  - 使用 margin 時 並不會變色，因為並不是 div 的範圍
  - 使用 padding 時會變色，因為 padding 算是 div 裡面的寬度
 - 如果設計給出來的寬是 400，因為 padding 跟 border 會改變，所以設定寬度時要重新計算

## box-sizing

```css
    webkit-boz-sizing : border-box;
    moz-box-sizing : border-box;
    box-sizing: border-box;
```

 - for IE 8 以上，主要是為了調整 box model 的計算方法，用 border 當成整個容器的最外框去重新計算寬度

## float 排版
 - 像是文繞圖的方式移到左邊或是移到右邊
 - 把它想像成 work 的文繞圖一樣，把圖片放在左邊的樣子，就把它設定 float = left，在調整文字的部份可以使用下面兩種方式：
  1. 用 margin 調整，設定文字 `margin-left = 圖片的寬度`，要注意如果有 border 時的寬度要加上去，不然會有對齊的問題
  2. 用 float 調整，文字直接用 `float = left`，有可能會有掉下來的問題，後面那個 (文字) 需要給它一個寬度
 - 如果要使用 float 排版的話，全部都要設定寬度，這樣子才會準確的排版
 - 使用 float 排版的話會比較精準，建議使用 float

## position
 - 設定的話就會變成像 float 一樣，變成浮動的 html
 - 設定 position = absolute (絕對)，html 原本的位置會消失，會從視窗的左上角開始排，可以使用 top 跟 left 排版，是從最左上角開始算，並不是從所在容器算
 - 設定 position = relative (相對)，會保留原本 html 的位置，並不會跳脫出原本所在容器，top 跟 left 值是從所在容器的左上角開始算，
 - 如果要用 position 排版的話，最外層需要設定 position = relative，這樣子裡面的有設定 position = absolute 的就會從外層容器開始算，不是從 視窗左上角開始算
 - 不用 position 排版的原因：
  1. 用太多的話會很混亂
  2. 如果內容太少的話，有可能會包不住設定 position = absolute 的容器

## display inline-block
 - 可以緊密排列，又有 block 的特性
 - 使用 float 的話需要 清除浮動，inline-block 的話就不用寫，它沒有浮動的問題
  - 上層如果是 `float = left`，清除的話就是 `clear = left`
  - 如果是用 `float = right`，就是 `clear = right`
  - 也可以寫 `clear = both`，就不用管是 left 還是 right
 - 使用 inline-block 的話，inline-block 跟 inline-block 之間會有固定間距，所以如果寬度相加起來是 100% 的話，就會因為間距而跑版。有兩種解法可以解決這個問題：
  1. 把 html 的 tag 連在一起就沒有間距
  2. 在 inline-block 的外層設定 `font-size = 0px`，就可以把 inline-block 的間距清掉，不過還要在裡面設定 font-size
 - 因為解法很麻煩，所以一般的排版不會用 inline-block 取代 float

## SMACSS - Module
 - 可以單獨存在而且可重複使用的元件
 - 如果拿掉也不會造成破版
 - 使用 class 定義 Module，不要用 id 跟 html tag
 - 定義子模組的話，在 父模組後面加上 - 作為名稱
  - `.menu` (父模組)
  - `.menu-submenu` (子模組)
  - `.menu-constrained` (子模組)

## 清除浮動時：
 - 可以加上 一個 div 設定 clear
 - 給外層容器設定一個高度就可以不用寫這個 div，不過這個 div 會受裡面的東西影響
 - 在外層寫 overflow = hidden，作用同 clear = both，可以清除 float 的浮動

## 排版相關注意事項：
 - menu 選單不是 div 區塊，建議使用 display-block 排版，而使用 margin 的話，就會填補原本間隙的位置
 - 如果 logo 裡面是 img，這個時候使用 float 不設寬度的話，就裡以裡面 img 的寬度為主，所以也可以不用設定寬度，不過還是習慣設定會比較好
 - 如果是有意義的圖片，就用 img 去作，沒有意義的話就用 background
 - 當設定了 padding 跟 margin 的時候，就要記得寬度可能需要調整
 - 可以省略的 class 就可以不用寫
 - 用 box-sizing 的話，可以把 width 改成用 % 比較方便
 - div 裡面只有 img 的話，圖片跟 div 之間會多出一點間距，這個時候可以把 img 的 display 設成 block 就不會有這個問題
 - a 底圖預設的大小是取決於文字
 - 寫比較多層的權重比較大，如果相同的話，比較先後順序
 - 如果大部份的 row 都一樣，只有一個不同的話，可以先對全部都設定一樣，在對小部份作單獨設定
 - nth-child(x) 找到 html 結構裡面的 第 x 個元素
 - 如果是橫向排列跑版的話，9 成跟 float 有關，通常是 width 或者是 overflow = hidden 的問題
 - 容器沒有包住原本的內容的話通常是 overflow = hidden 的問題

## SASS 修改 config.rb 建議
- css_dir => "css"
- javascripts_dir => "js"

## 如果是現有專案要導入 scss 的話
 1. 建議 css 路徑不要設定的跟 正常的一樣
 2. 建立 Compass 專案
 3. 複製原有的 css 到 stylesheets，改副檔名 .css 為 .scss
 4. reset 可以改用 compass 的，就可以不用自已寫了 `@import "compass/reset";`
 
### 如果要把 import 的檔案 compile 成一個檔案，就把 scss 的檔名 改成 "_" 開頭，這樣子就會變成一個檔案