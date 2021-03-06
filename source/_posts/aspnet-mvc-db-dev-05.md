---
title: ASP.NET MVC 使用資料庫開發 (五)
tags:
  - mvc
  - ef
categories: []
date: 2014-07-12 13:00:00
---

## 擴充資料模型 Matadata 的開發步驗

打開要擴充的 `.cs` 檔，
例如是 `客戶資料`，把 `tt` 檔下面的 程式碼全部 copy 起來

![](./aspnet-mvc-db-dev-05/01.png)

![](./aspnet-mvc-db-dev-05/02.png)

在 `Models 資料夾`下新增一個 class 叫 `客戶資料.Partial.cs`

![](./aspnet-mvc-db-dev-05/03.png)

把剛才的代碼貼上，會發現有錯誤，需要在作調整

![](./aspnet-mvc-db-dev-05/04.png)

- 1、把最上面的註解刪除
- 2、在類別名稱後面加上 `Metadata`，也就是 `客戶資料Metadata`
- 3、刪除 建構子

![](./aspnet-mvc-db-dev-05/05.png)

- 4、在現有的類別上面在建立一個 `Partial` 的類別，名稱跟原有要擴充的類別同名，也就是 `客戶資料`
- 5、在這個類別的上面套用 `MetadataType Attribute`，並指定是下面的 `客戶資料Metadata`，也就是 `[MetadataType(typeof(客戶資料Metadata))]`
- 備註：記得要 using `System.ComponentModel.DataAnnotations`

![](./aspnet-mvc-db-dev-05/06.png)

現在就可以在上面套用驗證屬性，不用擔心因為 `EF` 更新而被 Reset 了