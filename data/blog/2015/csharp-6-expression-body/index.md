---
title: C# - 6.0 Expression Body ( Functions and Properties )
description: C# 6.0 Expression Body ( Functions and Properties )
date: 2015-06-18 22:05:11.562+08:00
slug: "csharp-6-expression-body"
tags: [ c# ]
---

## Before C# 6

```csharp
class Test  
{
    private string name = "Cash";

    public Guid Id
    {
        get { return Guid.NewGuid(); }
    }

    public string GetName()
    {
        return this.name;
    }
}
```

## C# 6

```csharp
class Test  
{
    private string name = "Cash";
    public Guid Id => Guid.NewGuid();
    public string GetName() => name; 
}
```
