---
title: C# - 6.0 Exception Filters
description: C# 6.0 Exception Filters
date: 2015-08-01 21:02:01.961+08:00
slug: "csharp-6-exception-filters"
tags: [ c# ]
---

## Before C# 6

```csharp
static void Main ( string [ ] args )  
{ 
    try
    {
        doSomething();
    }
    catch (Exception ex) 
    {
        if (ex.Message == "DataNotFount")
        {
            Console.WriteLine("DataNotFount");
        }
        else if (ex.Message == "ChangePasswordError")
        {
            Console.WriteLine("ChangePasswordError");
        }
    }
} 
```

## C# 6

```csharp
static void Main ( string [ ] args )  
{ 
    try
    {
        doSomething();
    }
    catch (Exception ex) when (ex.Message == "DataNotFount")
    {
        Console.WriteLine("DataNotFount");
    }
    catch (Exception ex) when (ex.Message == "ChangePasswordError")
    {
        Console.WriteLine("ChangePasswordError");
    }
}
```