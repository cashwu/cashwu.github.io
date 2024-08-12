---
title: C# - 使用 Conditional 取代 if
description: C# 使用 Conditional 取代 if
date: 2015-05-16 08:16:19.267+08:00
slug: "csharp-conditional"
tags: [ c# ]
---

一般來說如果是 debug 跟 release 要呼叫或是處理的程式不同的時候，都會使用 `#if` 和 `#endif`
把只有 debug 時需要執行的程式包在裡面，不過其實這樣子的可讀性會比較不好

這個時候就可以使用 `Conditional` 這個 Attribute (namespace 為 `System.Diagnostics`)，
把 Debug 才需要執行的 Method 或是 class 上面套上這個 Attribute

下面來看實際的程式碼

使用 #if 時：

```csharp
class Program
{
    static void Main(string[] args)
    {
#if DEBUG
        GetValues();
#endif
        Console.ReadLine();
    }

    public static void GetValues()
    {
        Console.WriteLine("123");
    }
}
```

使用 Conditional 時：

```csharp
class Program
{
    static void Main(string[] args)
    {
        GetValues();
        Console.ReadLine();
    }

    [Conditional("DEBUG")]
    public static void GetValues()
    {
        Console.WriteLine("123");
    }
}
```

不過，Conditional 也不是沒有缺點

- 就算是 Release mode 時，有加上 Conditional 也是會出現在編譯後的 dll
- 只能套用在 class 和 void method 上面 (MSDN 裡面有寫)

大概說明了一下 Conditional 這個 Attribute，如果需要比較了解詳細的用法，請看參考連結

### 參考連結

- [MSDN Conditional (C# 程式設計手冊)](https://msdn.microsoft.com/zh-tw/library/4xssyw96.aspx)
- [MSDN 17.4.2 Conditional 屬性](https://msdn.microsoft.com/zh-tw/library/aa664622.aspx)
