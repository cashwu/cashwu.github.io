---
title: 'C# 6 Index Initializers'
tags:
  - 'c#'
categories: []
date: 2015-06-18 08:00:00
---

## Before C# 6

```csharp
static void Main ( string [ ] args )  
{ 
    var dic = new Dictionary<int, string>( );
    dic.Add( 1, "Cash" );
    dic.Add( 2, "Mary" );
} 

//or

static void Main ( string [ ] args )  
{ 
    var dic = new Dictionary<int, string>( ) 
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
    var dic = new Dictionary<int , string>( ) 
    { 
        [1] = "Cash", 
        [2] = "Mary"
    };
} 
```