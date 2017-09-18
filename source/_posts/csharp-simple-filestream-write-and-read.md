---
title: 'C# Simple FileStream Write and Read'
tags:
  - 'c#'
categories: []
date: 2015-05-27 08:00:00
---

## FileStream Write

```csharp
string s = "abc中文字";  
var buffer = Encoding.UTF8.GetBytes(s);  
var fs = new FileStream(@"Z:\test.txt", FileMode.Create);  
fs.Write(buffer, 0, buffer.Length);  
fs.Close();  
```

## FileStream Simple Read

在這裡暫不考慮讀進來的 Encoding 問題，所以直接用 UTF-8

```csharp
var fs = new FileStream(@"Z:\test.txt", FileMode.Open);  
var buffer = new byte[fs.Length];  
fs.Read(buffer, 0, buffer.Length);  
fs.Close();  
var s = Encoding.UTF8.GetString(buffer);  
```