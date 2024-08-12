---
title: C# - 6.0 Index Initializers
description: C# 6.0 Index Initializers
date: 2015-06-18 14:02:54.181+08:00
slug: "csharp-6-index-initializers"
tags: [ c# ]
---

## Before C# 6

```csharp
static void Main ( string [ ] args )  
{ 
    var dic = new Dictionary<int, string>();
    dic.Add( 1, "Cash" );
    dic.Add( 2, "Mary" );
} 

//or

static void Main ( string [ ] args )  
{ 
    var dic = new Dictionary<int, string>() 
    { 
        { 1, "Cash" }, 
        { 2, "Mary" } 
    };
} 
```

## C# 6

```csharp
static void Main ( string [ ] args )  
{ 
    var dic = new Dictionary<int , string>() 
    { 
        [1] = "Cash", 
        [2] = "Mary"
    };
} 
```