---
title: Rider EditorConfig csharp_new_line_before_members_in_object_initializers
description: 在上一篇 Rider 啟用 EditorConfig 中有提到一個神奇的設定，現在就要來講這個設定的神奇行為 csharp_new_line_before_members_in_object_initializers
date: 2022-08-06 21:38:19.683+08:00
slug: "rider_editorconfig_csharp_new_line_before_members_in_object_initializers"
tags: [ editorconfig , rider ]
---

在上一篇 Rider 啟用 EditorConfig 中有提到一個神奇的設定，現在就要來講這個設定的神奇行為 `csharp_new_line_before_members_in_object_initializers`

在微軟官方的說明網頁 [C# formatting options - csharp_new_line_before_members_in_object_initializers](https://docs.microsoft.com/en-us/dotnet/fundamentals/code-analysis/style-rules/csharp-formatting-options#csharp_new_line_before_members_in_object_initializers) 的地方有說明相關的設定，如果這個值為 `true` 的話，在 object initializers 的參數都會一行一個，如果是 `false` 的話，就是全部不換行，如下面的程式碼

- true

```csharp
var z = new B()
{
    A = 3,
    B = 4
}
```

- false

```
var z = new B()
{
    A = 3, B = 4
}
```

實際在 Rider 裡面測試 (ver 2022.1, var 2022.2)，這個參數設定為 `true` 排版的話，就會自動變成一行，測試過幾次，不管在 Windows 還是 Mac 的版本都是一樣，可以看一下我錄的操作

{{< youtube lLcELkIs_Yw >}}

不確定是不是 Rider 的問題還是 EditorConfig 的問題，我也沒有用 VS 測試過
就是因為這個參數我找了很久，為什麼我的排版會有問題....