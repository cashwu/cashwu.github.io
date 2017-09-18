---
title: 'C# 6 Interpolated Strings'
tags:
  - 'c#'
categories: []
date: 2015-06-15 08:00:00
---

## Before C# 6

```csharp
static void Main ( string [ ] args )  
{ 
    var h = DateTime.Now.Hour; 
    var m = DateTime.Now.Minute; 
    Console.WriteLine ( "Now is {0}:{1}" , h , m ); //Now is 2:12
} 
```

## C# 6

```csharp
static void Main ( string [ ] args )  
{ 
    var h = DateTime.Now.Hour; 
    var m = DateTime.Now.Minute; 
    Console.WriteLine ( $"Now is {h}:{m}" ); //Now is 2:12
}

//不足兩位數時前方將自動補 0
static void Main ( string [ ] args )  
{ 
    var h = DateTime.Now.Hour; 
    var m = DateTime.Now.Minute; 
    Console.WriteLine ( $"Now is {h:00}:{m:00}" ); //Now is 02:12
}
```