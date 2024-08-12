---
title: C# - Easy Convert Array from XML Format
description: C# Easy Convert Array from XML Format
date: 2015-06-14 22:20:47.718+08:00
slug: "csharp-easy-convert-array-from-xml-format"
tags: [ c# ]
---

## XML File

```xml
<?xml version="1.0" encoding="utf-8"?>  
<Settings>  
    <Points>
        <int>1</int>
        <int>2</int>
    </Points>
</Settings>  
```

## Mapping Class

```csharp
[XmlRoot( "Settings" )]
public class Settings  
{
    [XmlArray("Points")]
    [XmlArrayItem("int")]
    public int[] Points { get ; set ; }
}
```

## 注意事項

> 使用特定的 Xml Attribute 時注意是否需要 using