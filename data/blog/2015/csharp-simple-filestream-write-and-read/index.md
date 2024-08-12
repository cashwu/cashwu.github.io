---
title: C# - Simple StreamWriter and StreamReader
description: C# Simple StreamWriter and StreamReader
date: 2015-05-27 08:13:24.685+08:00
slug: "csharp-simple-filestream-write-and-read"
tags: [ c# ]
---

## StreamWriter

```csharp
string s = "abc 中文字 132";  
StreamWriter sw = new StreamWriter(@"Z:\test.txt", false);  
sw.Write(s);  
sw.Close();  
```

## StreamReader

```csharp
StreamReader sr = new StreamReader(@"Z:\test.txt");  
string s = sr.ReadToEnd();  
sr.Close();  
```