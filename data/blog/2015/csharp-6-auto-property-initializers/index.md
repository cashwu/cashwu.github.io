---
title: C# - 6.0 Auto Property Initializers
description: C# 6.0 Auto Property Initializers
date: 2015-06-17 22:09:06.744+08:00
slug: "csharp-6-auto-property-initializers"
tags: [ c# ]
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