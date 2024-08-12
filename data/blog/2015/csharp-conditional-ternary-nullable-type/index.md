---
title: C# - 三元運算式 & Nullable
description: C# 三元運算式 & Nullable
date: 2015-01-24 08:25:02.851+08:00
slug: "csharp-conditional-ternary-nullable-type"
tags: [ c# ]
---

一般來說判斷條件後給變數值的寫法通常是用 `if else` 

```csharp
var str = "";
if (condition)
{
    str = "abc";
}
else 
{
    str = "123";
}
```

如果判斷式和給值沒有什麼邏輯的話，可以改成用三元運算式來寫

```csharp
var str = condition ? "abc" : "123"; 
```

不過，如果今天變數為 `nullable of int` 型別的話，要給 `null` 時就會出錯，錯誤的訊息為 `無法確認條件運算式的類型，因為 '<null>' 和 'int' 兩者間沒有隱含轉換` 

```csharp
int? price = condition ? null : 1;
```

一般來說如果遇到這個問題，可能會改成下面的寫法，直接用 0 來取代 `null`
或是改用 `if else` 來判斷

```csharp
int? price = condition ? 0 : 1;
```

不過，如果說一定要給 `null` 為預設值的話，就可以用 `default` 這個關鍵字

```csharp
int? price = condition ? default(int?) : 1;
```

( 比較要注意的是， `default` 裡面的型別要記得給 `?` 就是 `nullable` 的型別才不會出錯 )

### 後記

一開始遇到 `nullable` 的問題，就會改用 `if else` 的判斷來處理，直到有一天突然想到好像可以用 `default` 這個關鍵字來處理預設值的問題，筆記一下...
