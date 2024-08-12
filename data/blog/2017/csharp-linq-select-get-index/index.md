---
title: C# - linq select get index
description: C# - linq select get index
date: 2017-06-03 17:13:56.935+08:00
slug: "csharp-linq-select-get-index"
tags: [ c# ]
---

使用 Linq 的 select 時要拿到資料 index 的寫法

```csharp
string[] fruits = { "apple", "banana", "mango", "orange", "passionfruit", "grape" };

var query = fruits.Select((fruit, index) => new { index, str = fruit.Substring(0, index) });
foreach (var obj in query)
{
    obj.Dump();
}
```

![](/images/404.webp)