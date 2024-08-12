---
title: C# 使用 Microsoft.VisualStudio.Threading.Analyzers 來檢查非同步程式
description: 在 c# 裡面寫非同步程式有的時候會不小心少了 await 或是命名沒有使用 Async 結尾，我們可以使用套件來幫我們找到這些問題
date: 2020-04-26 14:33:43.0+08:00
slug: "csharp-using-microsoft-visualstudio-threading-analyzers-valid-async"
tags: [ c# ]
---

> 這裡會使用到 Nuget 套件 [Microsoft.VisualStudio.Threading.Analyzers](https://www.nuget.org/packages/Microsoft.VisualStudio.Threading.Analyzers/)

在 c# 裡面寫非同步程式有的時候會不小心少了 `await` 或是命名沒有使用 `Async` 結尾，我們可以使用套件來幫我們找到這些問題

下面為範列程式

```csharp
public class Lib
{
    public void GetService()
    {
        var service = new Service();

        var result = service.Get().Result;

        Console.WriteLine(result);
    }

    public class Service
    {
        public Task<int> Get()
        {
            return Task.FromResult(123);
        }
    }
}
```

安裝套件完，Build 完就會引發 `warnings`

![](./01_4yXNFC.webp)

相關的檢查規則可以參考 [Github](https://github.com/microsoft/vs-threading/blob/master/doc/analyzers/index.md)