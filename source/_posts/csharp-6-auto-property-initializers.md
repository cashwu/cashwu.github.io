---
title: 'C# 6 Auto Property Initializers'
tags:
  - 'c#'
categories: []
date: 2015-06-17 08:00:00
---


## Before C# 6

```csharp
class Test  
{
    public Guid Id
    {
        get { return Guid.NewGuid(); }
    }
}
```

## C# 6

```csharp
class Test  
{
    public Guid Id { get; } = Guid.NewGuid();
}
```