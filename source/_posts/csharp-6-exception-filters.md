---
title: 'C# 6 Exception Filters'
tags:
  - 'c#'
categories: []
date: 2015-08-01 08:00:00
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
        else if    (ex.Message == "ChangePasswordError")
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
