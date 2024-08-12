---
title: SQL - StoreProcedure Input Date Parameter
description: SQL StoreProcedure Input Date Parameter
date: 2015-10-28 20:18:16.785+08:00
slug: "sql-storeprocedure-input-date-parameter"
tags: [ sql ]
---

今天寫程式時，遇到傳給 SqlServer 的 SP 參數，不知道是要使用 `DateTime.Now` 比較好，還是使用 `DateTime.Today` 比較好。如果 Where 條件就只要等於那一天就好了，從這個方面來看，好像使用 `DateTime.Today` 會比較好也比較直覺，真的是這樣子嗎 ?? 讓我們看下去。

所以就寫個小測試程式來看一下不同的差異

下面為 Table 的 Schema 和 測試資料

![](/images/404.webp)

![](/images/404.webp)

下面為測試的三個 SP，原則上就傳入時的參數型態不同而已 (對應到 Table 裡面的三個時間的型態)

![](/images/404.webp)

![](/images/404.webp)

![](/images/404.webp)

下面為使用 Linqpad 測試的回傳結果

![](/images/404.webp)

![](/images/404.webp)

![](/images/404.webp)

其實很明顯可以看的出來，如果只是使用等於的話，除非傳入參數的型態和資料欄位的型態一樣都是 `Date`，而且程式端需要使用 `DateTime.Today` 傳入，不然的話都查不到資料。所以其實影響查詢的重點有三個：程式端參數、SP 參數和資料欄位，不光只有程式端注意就好了，SP 也是很大的重點

如果以程式端不管資料端怎麼寫的話，其實程式端應該是使用那一個來傳都沒有差，也就是說你根本不知道 (不在意) SP 是用什麼型態來接參數的。其實站在 SP 的角度來看的話，應該也是不管程式端傳什麼我還是要查的到資料，所以，我覺得這個問題的重點應該是 SP 要怎麼 Design 會比較好，而且比較查的到資料

```sql
DECLARE @fromDate Date, @toDate DATE;

SET @fromDate = DATEADD(dd ,DATEDIFF(dd, 0, @date), 0); -- 只有日期沒有時間  
SET @toDate = DATEADD(dd ,DATEDIFF(dd, 0, @date), 1); -- 只有日期沒有時間

SELECT @date;  
SELECT @fromDate;  
SELECT @toDate;

SELECT * FROM Test t  
WHERE t.Date >= @fromDate AND t.Date < @toDate;

SELECT * FROM Test t  
WHERE t.SmallDateTime >= @fromDate AND t.SmallDateTime < @toDate;

SELECT * FROM Test t  
WHERE t.DateTime >= @fromDate AND t.DateTime < @toDate;  
```

用這種方式的話，就都可以查的到資料，也不用在意 SP 使用什麼 Parameter 或是程式端傳什麼進來了