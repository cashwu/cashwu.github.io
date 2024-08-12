---
title: Course - TDD Day 02
description: Course TDD Day 02
date: 2014-08-30 10:28:39.52+08:00
slug: "course-tdd-day-02"
tags: [  course ]
---

## 程式碼複雜度
 - 可以使用免費的 [Code Maid](http://www.codemaid.net/) 套件
 - 高標標準是 10
 - 低標標準是 15

## Web 重構流程
 1. Web 測試 - 重構前一定要有測試保護，程式碼不具可測試性，所以從粒度最大的 Web UI 測試開始建立
 2. Web 測試 - 將 Selenium IDE 錄製的腳本，放到測試專案中，由測試專案驅動執行測試
 3. 重構 - 註解 + 透過 ViewModel，讓程式邏輯與網頁 UI 分離 (原則上 MVC 專案應該是不用這一步)
 4. 重構 - 擷取方法，中文註解變成 method name
 5. 重構 - 職責分離（主動詞分離），將商業邏輯從網站抽到 library 中，如果主詞是頁面的話，就是這個頁面的 private method，如果不是的話，就抽出主詞成 class，動詞成 method
 6. 單元測試 - 為商業邏輯建立單元測試程式
 7. 重構 - 擷取介面
 8. 重構 - 將生成物件的職責獨立出
 
> 先把想法寫成 code，測試不要管它過不過，有問題的話測試就會跟你說

---

> 抽離成 interface 的好處是，新增一個判斷的話，就新增一個 class 就好，如果邏輯有變而且大部份的程式跟原本的一樣，就可以繼承它並 override 原本的 method，如果不是的話就新增一個

## 重構 Tips
 - 重構前務必有測試保護
 - 小範圍重構的效益，比大範圍重構來的有效
 - 一次只作一件事，切勿邊重構邊加需求
 - 先有 code 在重構，比一開始設計時套用一堆 design pattern 來得精準

## RIP TDD (from Kent Beck)
 - Over-engineering (過度設計)
 - PI feedback (改善 api 的設計與可用性)
 - Logic errors (想的跟寫的不一樣，寫的跟需求不一樣)
 - Documentation (寫跟維護文件是痛苦的)
 - Feeling overwhelmed (找不到切入點)
  - 可以先寫想要的是什麼，這就是切入點，一開始寫 hard code，
  - 把要什麼東西寫出來，幫自已程式寫規格，這就是測試案例
 - Separate interface from implementation thinking (抽象設計)
 -  不管細節，重點是抽象 (非實作細即)
 - Agreement (確保已修正問題的證據)
 -  怎麼確定問題已經修改好，就是原本的測試
 - Anxiety (改東壞西的擔心受怕)
  - 測試

## TDD
 - TDD 的重點不是測試，而是可以一次可以解決上面所有的問題，如果用其它的方式可以一次解決上面的問題，就可以不用 TDD
 - 測試只是 TDD 延伸的產物，重點是需求跟產出
 - 把需求全部都寫成測試案例，目前只是不能建置而已
 - 代碼盡量全部都用自動產生，跑測試時就會得到 TDD 的第一個紅燈
 - 給我 Scenario (給我例子)，就是把紅燈變成綠燈

### 想像寫一個功能就是在拯救使用者

## 為什麼 TDD 不夠
 1. 開發的產品不符合使用者需求
 2. 浪費無謂的成本
 3. 雞同鴨講、互相敵對

> 程式不是寫給自已爽的，還是要符合使用者需求

---

> 三位一體開發就是 BDD

## TDD is Action : ATDD (Acceptance) + BDD + TDD
- top down, don't bottom up

## What BDD ?
 - 從行為面用人話描述系統功能
 - 從人話自動繫結程式執行流程
 - User Story 與需求

> 把你想做的紀錄下來，大家都看的到也看的懂

## Why BDD ?
 - 都用人話溝通
 - 人話可以轉換成程式
 - 可以滿足使用者需求

## Specflow - Cucumber .NET 分支
 - Scenario 裡面的 Given 對應 Arrange，When 對應 Act，Then 對應 Assert
 - 中斷點通常下在 when 的地方

> code 寫完後，如果需求要改的話就要討論 Scenario

---

> 要寫任何一段 code 都要有他的原因在 (都需要有紅燈變綠燈的過程)

### 撰寫 step 中的測試程式，強迫思考 production code 的設計
- 類別名稱
- 建構式
- 方法名稱
- 參數名稱
- …

> 要記住 Scope 預設是全域的

## What You Learn

- 相同的 Step 可以重複使用
- Domain Know-how 從 Scenario 中浮現
- 碰到 Scenario 沒有的英文就建 詞彙表，之後名詞就從這裡來
- 有幾種 Scenario 一目了然
- Scenario 的 argument 可以自動轉型

- specflow 刪除最後一個直槓，在重打就會排版
- specflow，要有多筆情況使用同一個 Scenario 時，就要用 Outline 搭配 Examples
- WebTest 沒有頁面時，可以使用 PageObject
- 整合測試只管入口跟出口，不管裡面的細節，而 Unit Test 就是在解決裡面的的問題

## 一般來說 asp.net mvc Model 會分成
- Service - 改成 DI (IoC)
- DAO - 建 UnitTest

- 如果你的 Scrum 只是作作 Daily Meeting，貼貼便利貼，Production Code 沒有作 UnitTest，也沒有抽出 Interface，那你是在作什麼 scrum，充其量只是在玩大富翁
- 測試時 not null 的值一定要給，其它的可以不理它
- 引誘 po 講出實例
- BeforeScenario 跟 AfterScenario 都要刪除測試資料

## BDD
 - 用人話來說明需求
 - 用人話來描述測試案例
 - 用人話來程式

### 好課程請參考 [SkillTree](http://skilltree.my/)