---
title: 'C# 6 Expression Body (Functions and Properties)'
tags:
  - 'c#'
categories: []
date: 2015-06-18 08:00:00
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