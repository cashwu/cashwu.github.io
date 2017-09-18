---
title: 'C# Simple StreamWriter and StreamReader'
tags:
  - 'c#'
categories: []
date: 2015-05-27 08:00:00
---


## StreamWriter

```csharp
string s = "abc中文字132";  
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