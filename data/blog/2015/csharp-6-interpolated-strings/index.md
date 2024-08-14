---
title: C# - 6.0 Interpolated Strings
description: C# 6.0 Interpolated Strings
date: 2015-06-15 22:12:30.006+08:00
slug: "csharp-6-interpolated-strings"
tags:  [ c# ]
---

## Before C# 6

```csharp
static void Main ( string [ ] args )  
{ 
    var h = DateTime.Now.Hour; 
    var m = DateTime.Now.Minute; 
    Console.WriteLine ( "Now is {0}:{1}" , h , m ); 
    //Now is 2:12
} 
```

## C# 6

```csharp
static void Main ( string [ ] args )  
{ 
    var h = DateTime.Now.Hour; 
    var m = DateTime.Now.Minute; 
    Console.WriteLine ( $"Now is {h}:{m}" ); 
    //Now is 2:12
}

//不足兩位數時前方將自動補 0
static void Main ( string [ ] args )  
{ 
    var h = DateTime.Now.Hour; 
    var m = DateTime.Now.Minute; 
    Console.WriteLine ( $"Now is {h:00}:{m:00}" ); 
    //Now is 02:12
}
```